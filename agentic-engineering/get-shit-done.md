---
URL: https://github.com/gsd-build/get-shit-done
Gespeichert: 2026-04-22
---

# get-shit-done (GSD)

**Repo:** https://github.com/gsd-build/get-shit-done
**Von:** TÂCHES
**Stars:** ~56k

_Rekonstruiert aus [gsd-build/get-shit-done README](https://github.com/gsd-build/get-shit-done), 2026-04-22._

## Was ist es?

Meta-Prompting, Context Engineering und Spec-Driven Development als Slash-Command-System für Claude Code (und andere Agents).

> "Solves context rot — the quality degradation that happens as Claude fills its context window."

> "If you know clearly what you want, this WILL build it for you. No bs."

Kein Sprint-Theater, keine Story Points. Idee beschreiben → System extrahiert Kontext → Claude Code baut es.

## Installation

```bash
npx get-shit-done-cc@latest
```

Wählt Runtime (Claude Code, Cursor, Gemini CLI, Copilot, Windsurf, …) und Scope (global oder projekt-lokal). Installiert als Skills unter `.claude/skills/`.

Verify: `/gsd-help`

## Kernbefehle

| Command | Beschreibung |
|---------|-------------|
| `/gsd-new-project` | Projekt initialisieren + Planning-Struktur aufbauen |
| `/gsd-map-codebase` | Bestehende Codebase scannen und indexieren |
| `/gsd-spike` | 2–5 fokussierte Experimente mit Given/When/Then-Verdicts |
| `/gsd-sketch` | 2–3 interaktive HTML-Mockup-Varianten je Designfrage |
| `/gsd-help` | Befehlsübersicht |

Ergebnisse von Spike und Sketch landen in `.planning/`.

## Was es löst

**Context Rot:** Je mehr Claude produziert, desto schlechter wird die Qualität — weil der Kontext zugemüllt wird. GSD hält Claude auf Kurs durch strukturiertes Prompt-Engineering im Hintergrund.

**Scope Creep / Schema Drift:** Eingebaute Quality Gates:
- Schema drift detection (ORM-Änderungen ohne Migration)
- Security enforcement (Verifikation gegen Threat Models)
- Scope reduction detection (Planner darf keine Requirements still fallen lassen)

## Abgrenzung zu Vergleichbaren

Ähnlich wie [GitHub Spec Kit](spec-kit.md) und BMAD, aber explizit gegen Enterprise-Theater positioniert: kein Jira-Workflow, keine Sprint-Zeremonien. Komplexität im System, nicht im Workflow des Users.

> "I've done SpecKit, OpenSpec and Taskmaster — this has produced the best results for me."

---

#spec-driven-development #context-engineering #meta-prompting #claude-code #workflow #open-source
