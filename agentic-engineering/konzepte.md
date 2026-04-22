# Konzepte & Grundlagen

Semantic Contracts, Spec-Driven Development, Bugfixing-Ansätze.

## Artikel

- [Semantic Contracts](semantic-contracts.md) — Semantic Anchors zu neuen Begriffen komponieren statt LLM-Verhalten hoffen
- [GitHub Spec Kit](spec-kit.md) — Spec-Driven Development: 7-Schritt-Workflow, executable Specs, CLI-Tool
- [get-shit-done (GSD)](get-shit-done.md) — Meta-Prompting + Context Engineering für Claude Code; löst Context Rot; kein Enterprise-Theater
- [AI-gestützter Bugfixing-Workflow](ai-bugfixing-workflow.md) — Erst verstehen, nicht fixen — KI als Analyse-Kollege statt Code-Generator
- [Feedback Flywheel](feedback-flywheel.md) — Team-Lernen systematisieren: 4 Signal-Typen, lebende Artefakte (AGENTS.md, Playbooks), 4 Kadenzen (Fowler/Thoughtworks)
- [Cockburn: Spielt Code-Qualität noch eine Rolle?](cockburn-codequalitaet-llm.md) — Provokation + Token-Kostenvergleich DDD vs. kompakter Code; Kernthese: Entanglement ist teuer, nicht Größe

## Konzept-Vertiefungen (concepts/)

- [The Evolution: Waterfall → Scrum → Agentic](concepts/evolution.md) — Das invariante Muster: Geschwindigkeit erzwingt Struktur, nicht weniger
- [Guardrails](concepts/guardrails.md) — Static, Dynamic, Semantic Guardrails; Design-Prinzipien; Feedback-Loop in den Agent
- [Evals](concepts/evals.md) — Correctness, Behavior, Regression, Robustness Evals; Eval Harness Aufbau; CI-Integration
- [Agent Contracts: AGENTS.md + OpenAPI](concepts/contracts.md) — AGENTS.md als Agent-Interface; OpenAPI als maschinenlesbare API-Contracts
