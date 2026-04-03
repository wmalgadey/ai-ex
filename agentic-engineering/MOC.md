# Agentic Engineering — Map of Content

Konzepte und Praxis rund um agentic software development: Verifikation, Struktur, Workflows, Koordination.

## Artikel

- [mcs — Managed Claude Stack](mcs-managed-claude-stack.md) — macOS CLI für portable Claude Code Konfigurationen via Tech Packs und YAML
- [AI-gestützter Bugfixing-Workflow](ai-bugfixing-workflow.md) — Erst verstehen, nicht fixen — KI als Analyse-Kollege statt Code-Generator
- [Alistair Cockburn — Hexagonal Architecture mit Claude](alistair-cockburn-hexagonal-claude.md) — Ports & Adapters + Walking Skeleton als Claude Code Command
- [BMAD Method](bmad-method.md) — Open-Source Framework: 34+ Workflows, 12+ spezialisierte Agenten, vollständiger Dev-Lifecycle
- [Claude Code Remote Control](claude-code-remote-control.md) — Lokale Claude Code Session vom Phone steuern, nur outbound HTTPS, kein Port-Forwarding
- [Secrets Handling mit Claude Code](claude-code-secrets-handling.md) — 6 Methoden: permissions.deny, Sandbox, direnv, 1Password, SOPS + age
- [Claude Code vs. GitHub Copilot — 6 Config Layers](claudecode-vs-copilot-config-layers.md) — Vergleich der Konfigurations-Schichten beider Tools, Konvergenzpunkte
- [LSP + LLM: Code-Verständnis für AI-Agents](lsp-llm-code-understanding.md) — LSP-MCP-Bridges, Keel, GitLab Knowledge Graph als semantische Schichten
- [Panaversity: The AI Agent Factory](panaversity-agent-factory.md) — Spec-Driven Blueprint für "Digital FTEs", Buch + KI-Tutor + Plugin
- [GitHub Spec Kit](spec-kit.md) — Spec-Driven Development: 7-Schritt-Workflow, executable Specs, CLI-Tool
- [Claude Code Best Practice](claude-code-best-practice.md) — Feature Map, Orchestration-Hierarchie, Workflow- und Debugging-Patterns
- [5 Agent Skill Design Patterns](skill-design-patterns.md) — Tool Wrapper, Generator, Reviewer, Inversion, Pipeline — komponierbar
- [10 Agent Harness Patterns](agent-harness-patterns.md) — Crash Resume, Undo Chain, Patient Wait, Autonomy Dial und 6 weitere
- [Semantic Contracts](semantic-contracts.md) — Semantic Anchors zu neuen Begriffen komponieren statt LLM-Verhalten hoffen
- [Das Gehirn als Designmodell für Agenten](brain-system1-system2-agents.md) — System 1/2 nach Kahneman als Rahmen: wann LLM, wann Regelautomatisierung
- [Multi-Agent-Koordination: Selbstorganisation schlägt Orchestrierung](multi-agent-coordination-study.md) — 25.000 Tasks, 8 Protokolle: 14% besser ohne Hierarchie, 44% Gap zwischen Extremen
- [Drop the Hierarchy: Self-Organizing Agents](self-organizing-agents-no-hierarchy.md) — Paper-Zusammenfassung: starke Modelle brauchen weniger Struktur, nicht mehr

## Unterordner

### concepts/

- [The Evolution: Waterfall → Scrum → Agentic](concepts/evolution.md) — Das invariante Muster: Geschwindigkeit erzwingt Struktur, nicht weniger
- [Guardrails](concepts/guardrails.md) — Static, Dynamic, Semantic Guardrails; Design-Prinzipien; Feedback-Loop in den Agent
- [Evals](concepts/evals.md) — Correctness, Behavior, Regression, Robustness Evals; Eval Harness Aufbau; CI-Integration
- [Agent Contracts: AGENTS.md + OpenAPI](concepts/contracts.md) — AGENTS.md als Agent-Interface; OpenAPI als maschinenlesbare API-Contracts

### resources/

- [Links: Agentic Engineering](resources/links.md) — Kuratierte Links zu Evals-Tools, Security-Scannern, Mutation Testing, Code Health

### templates/

- [AGENTS.md Template](templates/AGENTS.md) — Vollständiges Template für projektweite Agent-Anweisungen
- [Eval Coverage Checklist](templates/eval-checklist.md) — Checkliste für Golden Dataset, Scorer, CI-Integration, Regression
