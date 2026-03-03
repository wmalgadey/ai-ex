# Secrets Handling mit Claude Code

## Das Problem

Claude Code liest standardmäßig alle Dateien im Arbeitsverzeichnis — inklusive `.env`, `.env.local`, `config/credentials.json` etc.  
Das LLM sieht dann API Keys, Passwörter, Tokens im Kontext. Das ist ein Sicherheitsrisiko, besonders wenn:
- Claude Code in CI/CD läuft
- Man Sub-Agents oder MCP-Server einsetzt
- Logs oder Sessions gespeichert werden

## Lösung 1: `permissions.deny` in `.claude/settings.json` (offizielle Methode)

Die direkte Lösung aus den offiziellen Docs:

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)",
      "Read(./config/credentials.json)",
      "Read(./.aws/**)",
      "Read(./kubeconfig)",
      "Read(./.kube/**)"
    ]
  }
}
```

**Wichtig:**
- `.claude/settings.json` → ins Git commiten → gilt für alle Team-Mitglieder
- `.claude/settings.local.json` → gitignored → nur lokale Overrides

**Scope-Hierarchie (höher = stärker):**
1. Managed Settings (IT/Org-Level, unveränderlich)
2. Command Line Arguments
3. Local (`.claude/settings.local.json`)
4. Project (`.claude/settings.json`)
5. User (`~/.claude/settings.json`)

→ Deny-Regeln im Project-Scope schützen das ganze Team.

## Lösung 2: Sandbox `filesystem.denyRead`

Für strengere Isolation (OS-Level, nicht nur Claude-Tool-Level):

```json
{
  "sandbox": {
    "enabled": true,
    "filesystem": {
      "denyRead": [
        "~/.aws/credentials",
        "~/.kube/config",
        "~/.ssh/id_rsa"
      ]
    }
  }
}
```

**Unterschied zu `permissions.deny`:**
- `permissions.deny` blockiert Claude's eigene File-Tools (Read, Edit, ...)
- `sandbox.filesystem.denyRead` blockiert auf OS-Ebene — also auch was über Bash/Subprozesse lesbar wäre

## Lösung 3: Secrets über Shell-Environment injizieren (nicht per Datei)

Statt `.env`-Files: Secrets direkt als Shell-Variablen setzen, bevor Claude Code gestartet wird.

```bash
# direnv (.envrc) — wird von Shell geladen, nicht von Claude Code gelesen
export DATABASE_URL="postgresql://..."
export API_KEY="..."

# Dann Claude Code starten
claude
```

**Mit direnv:**
```bash
# .envrc (gitignored!)
export DATABASE_URL=$(cat ~/.secrets/db_url)
```

Claude Code erbt dann die Environment-Variablen, liest aber nie die Datei selbst.

## Lösung 4: Secret Manager (1Password, Vault, Doppler)

### 1Password CLI

```bash
# Secrets werden nie in Dateien geschrieben
op run --env-file=.env.template -- claude

# .env.template enthält nur Referenzen:
# DATABASE_URL=op://Private/MyDB/url
# API_KEY=op://Work/MyAPI/credential
```

### HashiCorp Vault

```bash
export API_KEY=$(vault kv get -field=value secret/myapp/api_key)
claude
```

### Doppler

```bash
doppler run -- claude
```

Doppler injiziert alle Secrets als Env-Vars — Claude Code sieht die Werte, liest aber keine Dateien.

## Lösung 5: `.gitignore` + `CLAUDE.local.md`

Für lokale Sandbox-URLs, Test-Credentials etc.:

```
# .gitignore
.env
.env.local
secrets/
CLAUDE.local.md
```

`CLAUDE.local.md` wird von Claude Code automatisch geladen und gitignored — gut für lokale Anweisungen die Secrets-Paths erklären, ohne die Secrets selbst zu enthalten.

## Empfohlener Setup (Defense in Depth)

```json
// .claude/settings.json (committen)
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)",
      "Read(./.aws/**)"
    ]
  }
}
```

```bash
# .envrc (direnv, gitignored)
export DATABASE_URL="..."
export API_KEY="..."
```

```
# .gitignore
.env
.env.*
secrets/
*.pem
*.key
```

**Checkliste:**
- [ ] `permissions.deny` für alle Secret-Dateien in `.claude/settings.json`
- [ ] Secret-Dateien in `.gitignore`
- [ ] Secrets über Shell/direnv/Secret Manager injizieren, nicht per File
- [ ] Bei CI/CD: Managed Settings oder `--dangerously-skip-permissions` vermeiden

## Was Claude Code trotzdem noch sehen kann

`permissions.deny` schützt vor Claude's File-Tools. Aber:
- Wenn Claude `cat .env` über Bash ausführt → das funktioniert noch (Bash ist ein anderes Tool)
- Deshalb Bash-Deny kombinieren: `"Bash(cat ./.env)"` oder Sandbox nutzen
- Auto Memory kann Inhalte cachen → `/memory` regelmäßig prüfen

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Bash(cat .env*)",
      "Bash(printenv)"
    ]
  }
}
```

## Lösung 6: SOPS + age — Lokaler verschlüsselter Vault (Empfehlung)

**SOPS** (getsops/sops) ist der richtige Ansatz wenn man einen lokalen, verschlüsselten "Vault" will — kein Server, kein Cloud-Dienst, einfach eine verschlüsselte Datei im Repo.

### Warum besser als .env

- Secrets liegen verschlüsselt im Git (nachvollziehbar, versioniert)
- Claude sieht nie den Klartext — weder die verschlüsselte Datei noch den entschlüsselten Inhalt
- Kein plaintext auf Disk: Entschlüsselung nur im Speicher via `exec-env`

### Setup mit age (einfachste Key-Provider)

```bash
# 1. age key generieren (einmalig)
age-keygen -o ~/.config/sops/age/keys.txt

# 2. .sops.yaml im Projekt anlegen
cat > .sops.yaml << EOF
creation_rules:
  - age: age1<dein-public-key>
EOF

# 3. Secrets verschlüsselt anlegen
sops .env.sops.yaml
# Öffnet Editor → YAML schreiben → beim Speichern wird verschlüsselt

# .env.sops.yaml sieht dann so aus (im Git):
# DATABASE_URL: ENC[AES256_GCM,data:...,type:str]
# API_KEY: ENC[AES256_GCM,data:...,type:str]
```

### Claude Code starten mit decrypted Env-Vars

```bash
# Secrets werden nur im Prozess-Memory entschlüsselt — nie auf Disk geschrieben
sops exec-env .env.sops.yaml -- claude
```

Claude Code erbt alle Env-Vars, sieht aber nie die SOPS-Datei selbst.

### Defense in Depth: SOPS + deny rules kombinieren

```json
// .claude/settings.json
{
  "permissions": {
    "deny": [
      "Read(./.env.sops.yaml)",
      "Read(./.env.sops.*)",
      "Read(./.sops.yaml)"
    ]
  }
}
```

Damit kann Claude:
- Den verschlüsselten Blob **nicht lesen** (deny rule)
- Die entschlüsselten Werte **nicht sehen** (nie auf Disk)
- Die Werte **trotzdem nutzen** (als Env-Vars im Prozess)

### Hooks vs. permissions.deny

Hooks (PreToolUse) können Read-Aufrufe auch abfangen und abbrechen — technisch also eine Alternative zu `permissions.deny`. Aber:

- `permissions.deny` ist einfacher, deklarativ, zuverlässiger
- Hooks sind besser für: **Audit-Logging** (jeden Read-Versuch auf sensitive Dateien loggen), oder dynamische Entscheidungen (z.B. abhängig von Branch oder Kontext)
- Für reines Blockieren: `permissions.deny` bevorzugen
- Für Logging + Blockieren: Hook + deny kombinieren

```bash
# Beispiel PreToolUse Hook zum Audit-Logging
# ~/.claude/hooks/pre-read-audit.sh
#!/bin/bash
INPUT=$(cat)
FILE=$(echo "$INPUT" | jq -r '.tool_input.path // ""')
if echo "$FILE" | grep -qE '\.(env|sops|pem|key)'; then
  echo "AUDIT: Claude attempted to read $FILE at $(date)" >> ~/.claude/secret-access.log
fi
```

### SOPS für Scripts nutzen

```bash
# Script mit decrypted secrets ausführen
sops exec-env .env.sops.yaml -- npm run deploy

# Einzelnen Wert abfragen
sops -d --extract '["API_KEY"]' .env.sops.yaml
```

## Links

- [Claude Code Settings Docs](https://code.claude.com/docs/en/settings)
- [Permissions & Sandboxing](https://code.claude.com/docs/en/settings#permission-settings)
- [SOPS (getsops)](https://github.com/getsops/sops)
- [age Encryption](https://github.com/FiloSottile/age)
- [1Password CLI](https://developer.1password.com/docs/cli/)
- [Doppler](https://docs.doppler.com/docs/cli)
- [direnv](https://direnv.net/)

---
*Erstellt: 2026-03-03 | Aktualisiert: 2026-03-03*
