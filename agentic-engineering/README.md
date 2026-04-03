# Agentic Engineering

> "More speed forces more structure. Not less."
> — Florian Burka

## The Evolution

| Era | Cycle Time | Bug Discovery | Response |
|---|---|---|---|
| Waterfall | 6–18 months/release | Late, expensive | More planning, more gates |
| Scrum | 2–4 weeks/sprint | Faster, cheaper | CI/CD, unit/integration/E2E tests |
| Agentic Coding | Hours/days | Faster still | Full verification stack (see below) |

Each step accelerates. Each step produces more changes, more features, more bugs per unit time — but also faster correction. The pattern is always the same: **the thing that slows you down is insufficient structure, not insufficient speed.**

## What Agentic Engineering Requires

> "Everything Scrum wished it had is now mandatory."
> — Florian Burka

**Baseline (non-negotiable):**
- CI/CD pipeline
- Unit, Integration, E2E tests
- Linter + Code Health Scores (as automatic feedback loop *back into the agent*)

**Agentic-specific additions:**
- SAST (Static Application Security Testing)
- DAST (Dynamic Application Security Testing)
- Security Scans
- Mutation Testing
- Evals (LLM-specific quality checks)
- OpenAPI Specs (machine-readable contracts)
- `AGENTS.md` in every repo (agent contract — for humans AND agents equally)

## The Real Levers

The model is not the secret. What actually creates leverage:
- **Clear goals** — agents fail on vague specs, not on code
- **Guardrails** — constraints that make wrong outputs impossible or visible
- **Evals** — systematic verification that the output is actually correct
- **Domain expertise** — garbage in, garbage out, faster

## Themen

- [Patterns & Architekturen](patterns-und-architekturen.md) — Harness-Patterns, Agent-Koordination, Self-Organizing, Brain-Modell
- [Claude Code & Werkzeuge](claude-code-und-werkzeuge.md) — Best Practices, Remote Control, Secrets, Config, LSP, MCS
- [Konzepte & Grundlagen](konzepte.md) — Semantic Contracts, Spec-Driven Dev, Evals, Guardrails, Contracts

## Unterordner

```
concepts/     — Vertiefungen zu Grundkonzepten (evolution, guardrails, evals, contracts)
templates/    — AGENTS.md Template, Eval-Checkliste
resources/    — kuratierte externe Links
```

#agentic-engineering #software-development #ci-cd #evals #guardrails