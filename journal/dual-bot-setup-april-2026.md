# Dual-Bot Setup: Zaphod (OpenClaw) + Marvin (NanoClaw) parallel

_April 2026_

---

## Ausgangslage

Zwei KI-Assistenten laufen parallel auf demselben Linux-Server (Ubuntu):

- **Zaphod** (OpenClaw) — etabliert, vollständig eingerichtet, eigener Telegram-Bot, direkter Host-Zugriff
- **Marvin** (NanoClaw) — sandboxed Docker-Container, separater Telegram-Bot

Unterschiedliche Personas, unterschiedliche Telegram-Bots, unterschiedliche Zugriffsebenen — kein Konflikt.

---

## Architektur

### Zaphod (OpenClaw)

```
Telegram (Bot A) → OpenClaw Gateway (Port 18789)
                          ↓
                   Claude Agent (Anthropic API)
                          ↓
                   Workspace: ~/.openclaw/workspace
```

- Läuft als systemd user service `openclaw-gateway`
- Konfiguration: `~/.openclaw/openclaw.json`
- Workspace-Memory: `~/workspace/MEMORY.md`, `memory/YYYY-MM-DD.md`
- Git-Backup: GitLab auf `dev-pod01` (Tailscale)
- Exec-Approvals: per Telegram aktiviert (`approvals.exec` + `channels.telegram.execApprovals`)

### Marvin (NanoClaw)

```
Telegram (Bot B) → NanoClaw Orchestrator
                          ↓
              Docker Container (nanoclaw-agent:latest)
                          ↓
                   ANTHROPIC_BASE_URL=http://localhost:10254
                          ↓
                   OneCLI Gateway (Port 10254)
                          ↓
                   Anthropic API
```

- Läuft als systemd user service `nanoclaw`
- Codebase: `~/nanoclaw/` (Fork von `qwibitai/nanoclaw`, eigener Fork `wmalgadey/nanoclaw`)
- Agents laufen in isolierten Docker-Containern — filesystem isolation, nicht nur application-level
- Credentials werden über OneCLI verwaltet, nie direkt im Container
- Per-Gruppe isolierter Filesystem-Mount: `groups/telegram_main/`
- Zusätzliche Mounts: `~/repos` (read-write), `blogwatcher` CLI

### OneCLI als Credential-Layer (Port 10254/10255)

NanoClaw nutzt **OneCLI** (`ghcr.io/onecli/onecli:latest`) als Credential-Proxy — läuft als Docker-Container (`onecli-app-1`) mit eigenem Postgres-Backend. Container bekommen `ANTHROPIC_BASE_URL=http://localhost:10254` — der echte API-Key wird erst in OneCLI injiziert.

- Web-Dashboard: Port 10255 (`/overview`) — Credentials hier verwalten
- Sicherheitsfeature: kompromittierter Agent-Container kann keinen API-Key extrahieren
- **Gotcha:** Wenn der OAuth-Token in der Anthropic Console gelöscht wird, muss er in OneCLI neu hinterlegt werden — nicht in der `.env`

---

## Obsidian headless

Obsidian läuft als systemd user service (`obsidian.service`) via Xvfb (headless, kein Display):

```
Xvfb :99 → Obsidian (snap) → obsidian-cli.sock
                                    ↓
                              ocli (CLI wrapper)
```

- Vault: `~/repos/private-vault` (2435 Dateien, 51 Ordner)
- CLI-Aktivierung: `~/.config/obsidian/obsidian.json` → `"cli": true` (nicht im UI setzbar wenn headless — musste manuell in JSON geschrieben werden)
- Wrapper: `~/.local/bin/ocli` setzt `DISPLAY=:99` und ruft `obsidian-cli` auf

---

## Claude Code Session (marv)

Für interaktive Claude Code Arbeit im NanoClaw-Ordner:

```
systemd user service: nanoclaw-claude
        ↓
tmux session: nanoclaw
        ↓
nanoclaw-session (wrapper script)
        ↓
claude (Claude Code CLI)
```

- Service: `~/.config/systemd/user/nanoclaw-claude.service`
- Wrapper: `~/.local/bin/nanoclaw-session` — hält Session bei Absturz am Leben, Auto-Restart
- CLI: `~/.local/bin/marv` — attach/status/restart/start/stop
- Problem gelöst: systemd hat minimalen PATH → `claude` nicht gefunden → vollständiger PATH + `XDG_RUNTIME_DIR` explizit gesetzt
- Problem gelöst: `claude` beendet sich ohne TTY → Wrapper mit while-loop hält tmux-Session offen

### marv CLI

```bash
marv          # attach zur tmux Session
marv status   # kompakte Übersicht aller Services + tmux
marv restart  # Service neu starten
marv --help   # Hilfe
```

Status-Output:
```
nanoclaw status
───────────────
  ✓ nanoclaw bot: running
  ✓ claude code service: running
  ✓ tmux session 'nanoclaw': running
```

tmux Shortcuts (in Statusbar eingeblendet):
- `Ctrl+B D` — detach (Session läuft weiter)
- `Ctrl+B [` — Scroll-Modus (`Q` zum Beenden)

---

## Exec Approvals

OpenClaw verlangt für Shell-Befehle eine Bestätigung. Aktiviert über:

```json
"approvals": {
  "exec": {
    "enabled": true,
    "mode": "session",
    "targets": [{ "channel": "telegram", "to": "<YOUR_TELEGRAM_USER_ID>" }]
  }
},
"channels": {
  "telegram": {
    "execApprovals": {
      "enabled": true,
      "approvers": ["<YOUR_TELEGRAM_USER_ID>"]
    }
  }
}
```

Approval-Anfragen kommen als Telegram-Nachricht mit `/approve <id> allow-once|allow-always|deny`.

> Hinweis: Telegram User-IDs und Bot-Tokens gehören nicht ins Repo — in `.env` oder Secrets-Manager auslagern.

---

## Learnings

**Headless Obsidian:** `cli: true` muss direkt in die Electron-userData-Config (`~/.config/obsidian/obsidian.json`), nicht in den Vault. Obsidian öffnet den Unix-Socket erst wenn das Flag gesetzt ist. Lässt sich ohne UI setzen — Obsidian-Restart genügt.

**systemd + tmux + interaktive CLIs:** Interaktive Tools (Claude Code, etc.) brauchen ein TTY. `tmux new-session -d` liefert das. Aber: der gestartete Prozess darf sich nicht sofort beenden, sonst schließt tmux die Session. Wrapper-Script mit `while true` löst das.

**systemd PATH:** User-Services erben nicht den Login-Shell-PATH. Entweder vollen PATH in die Service-Unit schreiben oder `Environment=` verwenden.

**OneCLI als Credential-Layer:** NanoClaw nutzt OneCLI als Zwischenschicht zwischen Containers und Anthropic API. Credentials werden in OneCLI verwaltet (Web-UI auf Port 10255), Container sehen nie den echten Token. Minimiert Blast Radius bei Container-Kompromittierung. Wichtig: wenn der Token in der Anthropic Console rotiert/gelöscht wird, muss er in OneCLI neu gesetzt werden — nicht in der `.env`.

**Dual-Bot (Marvin + Zaphod):** Zwei Bots parallel auf einem Server funktioniert problemlos solange Telegram-Tokens getrennt sind. Keine gegenseitige Störung. Unterschiedliche Zugriffsebenen als Feature, nicht als Bug — Marvin sandboxed, Zaphod mit Host-Zugriff.

---

## Tags

#nanoclaw #openclaw #obsidian #tmux #systemd #claude-code #setup #infrastructure
