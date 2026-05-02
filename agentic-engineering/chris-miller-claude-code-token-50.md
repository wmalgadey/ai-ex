---
URL: https://www.linkedin.com/posts/chris-miller-786343221_i-cut-my-claude-code-token-usage-by-50-with-share-7456018263924244480-y0Th
Gespeichert: 2026-05-02
Autor: Chris Miller
---

# Claude Code Token-Verbrauch halbieren — 4 Stellschrauben

Konfigurationsstrategie in `CLAUDE.md` + `settings.json`, ~2 Minuten Setup.

---

**1. Subagent-Hierarchie nach Modellkosten**

Claude bekommt die Anweisung, für Teilaufgaben den günstigsten geeigneten Agenten zu spawnen:
- **Haiku** — mechanische Routineaufgaben
- **Sonnet** — Recherche, Code-Exploration
- **Opus** — komplexe Planung

Zwei Regeln verhindern Inflation: Haiku-Subagenten dürfen keine weiteren Agenten spawnen, maximale Spawn-Tiefe: 2.

**2. Tool-Präferenzen**

- `WebFetch` statt Screenshot-Tools für öffentliche Seiten (text-only, kostenlos)
- `agent-browser` CLI für dynamischen Content (~82% weniger Token als Screenshot-basierte Tools)
- PDF-Text-Extraktion statt `Read`-Tool

**3. settings.json**

- 1M-Context-Windows deaktivieren
- Auto-Compact bei 80% statt bei voller Kapazität

**Aufwand:** ~2 Minuten Setup, danach dauerhaft.

#claude-code #token-kosten #subagents #optimierung
