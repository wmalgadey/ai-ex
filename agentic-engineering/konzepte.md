# Konzepte & Grundlagen

Semantic Contracts, Spec-Driven Development, Bugfixing-Ansätze.

## Artikel

- [Semantic Contracts](semantic-contracts.md) — Semantic Anchors zu neuen Begriffen komponieren statt LLM-Verhalten hoffen
- [GitHub Spec Kit](spec-kit.md) — Spec-Driven Development: 7-Schritt-Workflow, executable Specs, CLI-Tool
- [get-shit-done (GSD)](get-shit-done.md) — Meta-Prompting + Context Engineering für Claude Code; löst Context Rot; kein Enterprise-Theater
- [AI-gestützter Bugfixing-Workflow](ai-bugfixing-workflow.md) — Erst verstehen, nicht fixen — KI als Analyse-Kollege statt Code-Generator
- [Feedback Flywheel](feedback-flywheel.md) — Team-Lernen systematisieren: 4 Signal-Typen, lebende Artefakte (AGENTS.md, Playbooks), 4 Kadenzen (Fowler/Thoughtworks)
- [Cockburn: Spielt Code-Qualität noch eine Rolle?](cockburn-codequalitaet-llm.md) — Provokation + Token-Kostenvergleich DDD vs. kompakter Code; Kernthese: Entanglement ist teuer, nicht Größe
- [Martin Fowler — SPDD](spdd-martin-fowler.md) — Prompts als First-Class-Artefakte; REASONS Canvas (7-gliedrig); "When reality diverges, fix the prompt first"
- [Ralf D. Müller — Semantic Anchors & SPDD](ralf-mueller-semantic-anchors-spdd.md) — LinkedIn-Post: Semantic Anchors + Spec-Driven Development als komplementärer Ansatz zu SPDD
- [Codereading Technique](codereading-technique.md) — Nicholas Gebo: strukturiertes Code-Lesen als eigenständige Produktivitätstechnik
- [Stimme als Text-Datei (Ruben Hassid)](ruben-hassid-youre-just-a-text-file.md) — Voice Profile: 100 Interview-Fragen → 20k Wörter → 2–5k Token; Kompressions-Test; Phrase Bank, Hard Refusals

## Konzept-Vertiefungen (concepts/)

- [The Evolution: Waterfall → Scrum → Agentic](concepts/evolution.md) — Das invariante Muster: Geschwindigkeit erzwingt Struktur, nicht weniger
- [Guardrails](concepts/guardrails.md) — Static, Dynamic, Semantic Guardrails; Design-Prinzipien; Feedback-Loop in den Agent
- [Evals](concepts/evals.md) — Correctness, Behavior, Regression, Robustness Evals; Eval Harness Aufbau; CI-Integration
- [Agent Contracts: AGENTS.md + OpenAPI](concepts/contracts.md) — AGENTS.md als Agent-Interface; OpenAPI als maschinenlesbare API-Contracts
