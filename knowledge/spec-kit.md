# GitHub Spec Kit

**Repo:** https://github.com/github/spec-kit
**Docs:** https://github.github.io/spec-kit/
**Von:** GitHub (official)

## Was ist es?

**Spec-Driven Development (SDD)** — Ein Open-Source Toolkit das Spezifikationen in den Mittelpunkt stellt statt Code.

> "Build high-quality software faster."
> "An open source toolkit that allows you to focus on product scenarios and predictable outcomes instead of vibe coding every piece from scratch."

**Kernidee:** Spezifikationen sind nicht nur Scaffolding — sie werden *executable* und generieren direkt funktionierende Implementierungen. Kein Vibe-Coding, sondern strukturierter Prozess.

## Workflow (7 Schritte)

1. **`/speckit.constitution`** — Governing Principles definieren (Code Quality, Testing Standards, Architektur-Leitlinien)
2. **`/speckit.specify`** — Was soll gebaut werden? (Focus auf das *Was*, nicht das *Wie*)
3. **`/speckit.clarify`** *(optional)* — Unterbestimmte Anforderungen klären
4. **`/speckit.plan`** — Tech Stack & Architekturentscheidungen → technischer Implementierungsplan
5. **`/speckit.analyze`** *(optional)* — Cross-Artifact Konsistenzprüfung
6. **`/speckit.tasks`** — Actionable Task-Liste generieren (mit Parallelisierungs-Markern `[P]`)
7. **`/speckit.implement`** — Ausführung aller Tasks

## Installation

```bash
# Persistent (empfohlen)
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Projekt initialisieren
specify init my-project --ai claude
# oder im aktuellen Verzeichnis
specify init . --ai claude
```

## Unterstützte AI Agents

Claude Code ✅, Cursor ✅, GitHub Copilot ✅, Gemini CLI ✅, Codex CLI ✅, Windsurf ✅, Roo Code ✅, und viele mehr. Generischer Modus für eigene Agents via `--ai generic`.

## Slash Commands

| Command | Beschreibung |
|---------|-------------|
| `/speckit.constitution` | Projekt-Prinzipien & Guidelines |
| `/speckit.specify` | Feature-Anforderungen & User Stories |
| `/speckit.clarify` | Klärung unklarer Anforderungen |
| `/speckit.plan` | Technischer Implementierungsplan |
| `/speckit.analyze` | Konsistenz- & Coverage-Analyse |
| `/speckit.checklist` | Quality Checklists generieren |
| `/speckit.tasks` | Aufgaben-Breakdown erstellen |
| `/speckit.implement` | Implementierung ausführen |

## Projektstruktur nach Init

```
.specify/
├── memory/
│   └── constitution.md
├── scripts/
├── specs/
│   └── 001-feature-name/
│       ├── spec.md
│       ├── plan.md
│       ├── tasks.md
│       ├── data-model.md
│       └── contracts/
└── templates/
```

## Voraussetzungen

- Python 3.11+, uv, Git
- Unterstützter AI Agent (Claude Code, Cursor, etc.)

## Warum interessant?

Perfekt für Wolfgangs Kombination aus Coding-Erfahrung + AI-Nutzung. Statt "Vibe Coding" gibt es strukturierte Spezifikationen die direkt in Implementierungen überführt werden — sehr ähnlich zu Clean Code / Pragmatic Programmer Philosophie. Von GitHub selbst, also production-ready gedacht.

Besonders interessant für Platform Engineering Projekte wo Anforderungen klar dokumentiert sein müssen.

---
*Gespeichert: 2026-02-25*
