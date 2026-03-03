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

## Links

- [Claude Code Settings Docs](https://code.claude.com/docs/en/settings)
- [Permissions & Sandboxing](https://code.claude.com/docs/en/settings#permission-settings)
- [1Password CLI](https://developer.1password.com/docs/cli/)
- [Doppler](https://docs.doppler.com/docs/cli)
- [direnv](https://direnv.net/)

---
*Erstellt: 2026-03-03*
