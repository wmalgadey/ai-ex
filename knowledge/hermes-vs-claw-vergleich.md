---
URL: https://hermes-agent.org/
Gespeichert: 2026-04-05
---

# Hermes Agent vs. NanoClaw vs. OpenClaw

Hermes (Nous Research) ist ein selbst-gehosteter autonomer Agent — ein direkter Vergleichspunkt zum eigenen Setup.

---

## Hermes Agent

**→ hermes-agent.org** — Nous Research, MIT, zero telemetry

Persistenter Heimserver-Agent mit Multi-Messenger-Anbindung (Telegram, Discord, Slack, WhatsApp, Signal) und lokalem Gedächtnis unter `~/.hermes/`. Kein Cloud-Zwang, kein SaaS-Lock-in.

Kernfähigkeiten:
- Persistentes Memory: Lernt über Sessions hinweg, keine Kontext-Wiederholung
- Skill-Generierung: Erzeugt wiederverwendbare Skill-Dokumente beim Lösen von Problemen
- Scheduler: Eingebaute Aufgabenplanung für Reports und Automationen
- Browser-Kontrolle: Web-Search, Page Extraction, Vision-Analyse
- Code-Ausführung: Lokal, Docker, SSH, Cloud

Stack: Linux/macOS/WSL2, unterstützt Nous Portal, OpenRouter und lokales vLLM. Einzeiler-Install.

---

## Vergleich

| Dimension | Hermes | NanoClaw (Marvin) | OpenClaw (Zaphod) |
|---|---|---|---|
| **Basis** | Nous Research (open) | Anthropic NanoClaw | Anthropic OpenClaw |
| **Model** | Wählbar (Nous, OpenRouter, lokal) | Claude (Anthropic) | Claude (Anthropic) |
| **Hosting** | Self-hosted auf eigenem Server | Docker-Container, sandboxed | Direkt auf Host |
| **Isolation** | Keine explizite Sandbox | Sandboxed per Default | Voller Host-Zugriff |
| **Messenger** | Telegram, Discord, Slack, WhatsApp, Signal | Telegram | Telegram |
| **Memory** | Persistentes lokales Memory (`~/.hermes/`) | Kein eingebautes Memory (Workspace-Files) | Kein eingebautes Memory |
| **Skills/Plugins** | Auto-generierte Skill-Dokumente | Plugin-System (custom Skills) | Minimal |
| **Scheduler** | Eingebaut | Eingebaut via MCP | Nicht bekannt |
| **Browser** | Eingebaut | `agent-browser` | Nicht konfiguriert |
| **Vault/Dateizugriff** | `~/.hermes/` | Mounts: ai-ex, private-vault | Obsidian-CLI via Wrapper |
| **Netzwerk** | Wie configured | Tailscale + Cloud Gateway Ultra | Tailscale |
| **Lizenz** | MIT | Proprietär (Anthropic) | Proprietär (Anthropic) |
| **Telemetrie** | Zero | Anthropic API-Calls | Anthropic API-Calls |

---

## Einordnung

Hermes und NanoClaw lösen dasselbe Problem — persistenter Assistent, Messenger-Anbindung, Automatisierungen — aber mit unterschiedlicher Philosophie.

**Hermes-Vorteil:** Model-Agnostik. Kein Vendor-Lock-in bei Anthropic. Lokale Modelle möglich. Das eingebaute Memory-System ist etwas, das bei Claw nachgebaut werden muss (via Workspace-Files oder externem Tool wie mem0).

**Claw-Vorteil:** Claude ist schlicht besser als die meisten Nous-Modelle für komplexe Reasoning-Tasks. Das Plugin/Skill-System ist flexibel erweiterbar. Das NanoClaw/OpenClaw-Doppel ermöglicht differenzierte Security-Profile auf derselben Maschine — Hermes macht das nicht.

**Wo Hermes interessant wird:** Als Fallback wenn Anthropic-API-Kosten zu hoch werden, oder für Multi-Messenger-Szenarien (WhatsApp/Signal-Anbindung fehlt bei Claw komplett).

_Stand: April 2026 — Hermes v1.x, NanoClaw 0.x_

#agents #vergleich #hermes #nanoclaw #openclaw #selbstgehostet #memory
