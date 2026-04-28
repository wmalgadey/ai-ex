---
URL: https://github.com/rtk-ai/rtk
Gespeichert: 2026-04-11
---

# rtk (rtk-ai)

CLI-Proxy: Reduziert LLM-Token-Verbrauch bei Dev-Commands um 60-90%. Transparent für Agenten.

## Problem

LLMs bekommen bei `git status`, `ls -la`, `npm test` etc. oft riesige, redundante Outputs. Das verbrennt massiv Tokens, die für den eigentlichen Kontext fehlen.

## Was rtk macht

Filtert und komprimiert Command-Outputs BEVOR sie den LLM-Kontext erreichen. Als Rust Binary, <10ms Overhead, 100+ unterstützte Commands.

**Strategien:** Smart Filtering, Grouping, Truncation, Deduplication.

**Beispiel-Ersparnisse:**
- `ls / tree`: -80%
- `cat / read`: -70%
- `git status`: -80%
- `cargo test / npm test`: -90%
- `docker ps`: -80%

## Installation & Nutzung

```bash
brew install rtk # oder install.sh / cargo install
rtk init -g      # Installiert Hooks für Claude Code, Copilot, Gemini CLI, Cursor, OpenCode etc.
```

Der Hook schreibt Bash-Commands transparent um (z.B. `git status` → `rtk git status`). Claude Code sieht die Umschreibung nicht, bekommt nur komprimierten Output.

## Features

- Spezifische Commands: `rtk ls`, `rtk read`, `rtk grep`, `rtk diff`, `rtk git status`, `rtk test cargo test` etc.
- Telemetrie (opt-out): anonyme Nutzungsdaten (Command-Counts, Token-Savings)
- `rtk gain`: Übersicht der Ersparnisse
- `rtk discover`: Findet ungenutzte Sparpotenziale
- `rtk doctor`: Scannt nach Cache-Bugs

## Relevanz

Sehr relevant für Claude Code (und auch OpenClaw mit passendem Plugin) um Token-Kosten zu senken und Kontext effizienter zu nutzen. Ergänzt clauditor.

#llm #token-optimization #cli #tooling #rust
