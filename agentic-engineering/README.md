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

Everything Scrum wished it had is now mandatory:

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

## Structure of This Directory

```
agentic-engineering/
├── README.md             ← this file
├── concepts/
│   ├── evolution.md      ← Waterfall→Scrum→Agents in depth
│   ├── guardrails.md     ← What guardrails are and how to design them
│   ├── evals.md          ← Evals: what, why, how
│   └── contracts.md      ← AGENTS.md + OpenAPI as agent contracts
├── templates/
│   ├── AGENTS.md         ← Template for project-level agent instructions
│   └── eval-checklist.md ← Checklist for eval coverage in agentic projects
└── resources/
    └── links.md          ← Curated external resources
```
