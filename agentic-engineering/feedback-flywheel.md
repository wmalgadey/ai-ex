---
URL: https://martinfowler.com/articles/reduce-friction-ai/feedback-flywheel.html
Gespeichert: 2026-04-09
---

# Feedback Flywheel

Rahul Garg (Thoughtworks), April 2026 — veröffentlicht auf martinfowler.com.

## Problem

Teams nutzen KI-Coding-Assistenten, aber Lernen bleibt individuell. Wer herausfindet wie man gut promptet, welche Workflows funktionieren, wo das Modell versagt — behält das für sich. Das Team als Ganzes macht keinen Fortschritt.

> "Each interaction generates signal that most teams discard."

## Kernidee: Living Infrastructure

Nicht einmalig aufgeschriebene Regeln, sondern aktiv gepflegte Artefakte:
- **Priming-Dokumente** (AGENTS.md, CLAUDE.md) — Kontext, den das Modell vor jedem Task braucht
- **Review-Commands** — wiederholbare Slash-Commands für häufige Prüfungen
- **Playbooks** — bewährte Interaktionssequenzen für wiederkehrende Aufgaben
- **Failure-Logs** — dokumentierte Fehlerursachen und Gegenmaßnahmen

## Vier Signal-Typen

| Signal | Quelle | Ziel |
|---|---|---|
| **Context** | Fehlendes Priming → schlechte Ausgabe | Priming-Dokument ergänzen |
| **Instruction** | Effektive Formulierung gefunden | Command-Bibliothek |
| **Workflow** | Erfolgreiche Interaktionssequenz | Playbook |
| **Failure** | Root Cause einer fehlgeschlagenen KI-Ausgabe | Failure-Log + Gegenstrategie |

## Vier Kadenzen

1. **Nach jeder Session** — 1 Minute: "Was sollte sich in unseren gemeinsamen Artefakten ändern?"
2. **Daily Standup** — 5 Minuten KI-Learnings
3. **Retrospektive** — systematische Auswertung der gesammelten Signale
4. **Periodisches Review** — Artefakte bereinigen, Veraltetes entfernen

## Metriken (qualitativ)

- Iteration Cycles bis zum akzeptierten Output
- First-Pass Acceptance Rate
- Ramp-up Zeit neuer Teammitglieder

## Verbindungen

- [Semantic Contracts](semantic-contracts.md) — CLAUDE.md/AGENTS.md als Shared Artifacts sind die Ziel-Infrastruktur
- [Agent Contracts: AGENTS.md + OpenAPI](concepts/contracts.md) — was befüllt wird
- [Claude Code Best Practice](claude-code-best-practice.md) — individuelle Ebene; Feedback Flywheel die Team-Ebene darüber

_Rekonstruiert aus dem Fowler-Artikel, 2026-04-09._

#team #feedback #learning #ai-assisted-development #priming #agile #thoughtworks
