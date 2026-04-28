---
URL: https://martinfowler.com/articles/structured-prompt-driven/
Gespeichert: 2026-04-28
---

# Martin Fowler — Structured-Prompt-Driven Development (SPDD)

_Publiziert: 28. April 2026_

> "How to make LLM-assisted changes governable, reviewable, and reusable"

Prompts als First-Class-Artefakte: versioniert, reviewed, wiederverwendet und iterativ verbessert — statt Ad-hoc-Chat-Interaktionen. Kernthese: LLMs beschleunigen individuelle Entwickler, erzeugen aber Reibung auf Systemebene (ambige Anforderungen, schwerer reviewbarer Code, mehr Integrationsrisiko).

## REASONS Canvas

Siebengliedrige Struktur die Prompts von Intent bis Governance führt:

| Buchstabe | Inhalt |
|---|---|
| **R**equirements | Problem Statement, Definition of Done |
| **E**ntities | Domain-Modell und Beziehungen |
| **A**pproach | Strategie zur Anforderungserfüllung |
| **S**tructure | System-Fit, Komponenten, Dependencies |
| **O**perations | Konkrete, testbare Implementierungsschritte |
| **N**orms | Engineering-Standards (Naming, Observability, Defensive Coding) |
| **S**afeguards | Non-Negotiables (Invarianten, Security, Performance) |

> "When reality diverges, fix the prompt first—then update the code."

Verwandt: [[semantic-contracts]] (Ralf D. Müller — Semantic Anchors als komplementärer Ansatz)

#spdd #spec-driven-development #prompt-engineering #agentic-engineering #martin-fowler #llm
