# Semantic Contracts

**Quelle:** https://lnkd.in/deAn2Wnb
**Gespeichert:** 2026-03-29

> "Write a specification" can mean anything. A Semantic Contract makes it precise.

Semantic Contracts sind Definitionen die dem LLM am Session-Start gegeben werden — nicht als Prompt Engineering, sondern als präzise Bedeutungszuweisung für Begriffe die im Training nicht existieren.

**Kernidee:** Bekannte Semantic Anchors (Begriffe die jedes LLM kennt: arc42, Gherkin, INVEST, OWASP) werden zu neuen Begriffen komponiert. Statt "Operations Manual" neu zu erklären, schreibt man: `Operations Manual = arc42 Section 8 + Runbook Pattern`.

## 12 veröffentlichte Contracts für einen kompletten Development-Workflow

| Phase | Contract-Komponenten |
|-------|---------------------|
| Requirements Discovery | Socratic Method + MECE + PRD |
| Specification | Gherkin + BDD |
| Architecture | arc42 + C4 + ADR (Nygard) + Pugh Matrix |
| Backlog | INVEST + MoSCoW |
| Implement Next | TDD London School + Conventional Commits + Definition of Done |
| Quality Review | Fagan Inspection + OWASP Top 10 + ATAM |
| Docs-as-Code | AsciiDoc + PlantUML + docToolchain |

Dazu drei Kommunikations-Contracts:
- **Concise Response** — BLUF (Bottom Line Up Front)
- **Simple Explanation** — Feynman Technique
- **Writing Style** — Wolf Schneider + custom rules

## Verwendung

Website → gewünschte Contracts auswählen → als `semantic-contracts.md` herunterladen → in `AGENTS.md` oder `CLAUDE.md` droppen.

_Generiert anhand von LinkedIn-Post, 2026-03-29._

#semantic-contracts #semantic-anchors #llm #agentic-engineering #prompt-engineering #claude-md
