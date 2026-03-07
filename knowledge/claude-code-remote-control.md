# Claude Code Remote Control

> Continue a local Claude Code session from your phone, tablet, or any browser.

Source: https://docs.anthropic.com/en/docs/claude-code/remote-control

## Was ist das?

Remote Control verbindet claude.ai/code oder die Claude Mobile App (iOS/Android) mit einer lokal laufenden Claude Code Session. Die Session läuft dabei **vollständig auf deinem Rechner** — Phone/Browser ist nur ein Fenster in die lokale Session.

Typischer Workflow (wie viral auf Twitter beschrieben):
1. Agent 1 erstellt Spec/Blueprint + Todo-Liste
2. Agent 2 bekommt den Blueprint und fängt an zu bauen
3. `claude remote-control` starten → QR-Code scannen → auf den Balkon gehen
4. Live-View auf dem iPhone, gelegentlich Feedback eintippen

## Setup

```bash
# Voraussetzungen:
# - Pro/Max/Team/Enterprise Plan (kein API Key!)
# - claude /login ausgeführt
# - einmal im Projektverzeichnis claude gestartet (Workspace Trust)

# Neue Session starten:
claude remote-control
claude remote-control "Mein Projekt"   # mit Name

# Aus laufender Session heraus:
/remote-control
/rc "Mein Projekt"    # Kurzform
```

QR-Code anzeigen: Leertaste drücken während `claude remote-control` läuft.

Für alle Sessions automatisch aktivieren: in Claude Code `/config` → "Enable Remote Control for all sessions" → true

## Verbinden

- **Session URL** direkt im Browser öffnen
- **QR-Code scannen** → öffnet in Claude App
- **claude.ai/code** → Session-Liste → Remote Control Sessions haben grünes Dot-Icon

## Security

Das ist der interessante Teil:

**Kein eingehender Port wird geöffnet.** Die lokale Claude Code Session macht ausschließlich **outbound HTTPS Requests** an die Anthropic API. Kein Port-Forwarding, kein ngrok, kein offener Server auf dem Rechner.

**Wie es funktioniert:**
1. `claude remote-control` registriert sich bei der Anthropic API (outbound)
2. Die Session **pollt** dann die API auf eingehende Nachrichten (Long Polling / Streaming)
3. Wenn du vom Phone verbindest, routet der Anthropic-Server die Messages zwischen deinem Phone und der lokalen Session
4. Alles läuft über TLS (HTTPS) — gleiche Transport-Security wie jede andere Claude Code Session

**Credentials:**
- Multiple short-lived credentials
- Jeder Credential ist auf einen einzigen Zweck beschränkt (scoped)
- Laufen unabhängig voneinander ab

**Was lokal bleibt:**
- Dein Filesystem
- MCP Server
- Tools und Project Config
- Die eigentliche Ausführung

**Was über Anthropic läuft:**
- Messages zwischen Phone und lokalem Client werden über die Anthropic API geroutet

## Unterschied zu "Claude Code on the Web"

| | Remote Control | Claude Code on the Web |
|---|---|---|
| Ausführung | Lokal auf deinem Rechner | Anthropic Cloud Infrastructure |
| Filesystem | Dein lokales FS | Anthropic-managed |
| MCP Server | Verfügbar | Nicht verfügbar |
| Use Case | Unterwegs weiterarbeiten | Task ohne lokales Setup starten |

## Einschränkungen

- **Eine Remote-Verbindung** pro Claude Code Session
- **Terminal muss offen bleiben** — Remote Control ist ein lokaler Prozess; Terminal schließen = Session Ende
- **Netzwerkausfall >~10 Minuten** → Session Timeout, dann neu starten

## Flags

```bash
claude remote-control --name "My Project"   # Custom Name
claude remote-control --verbose             # Connection Logs
claude remote-control --sandbox             # Filesystem/Network Isolation
claude remote-control --no-sandbox          # Sandboxing explizit deaktivieren
```

---

*Hinzugefügt: 2026-03-07*
