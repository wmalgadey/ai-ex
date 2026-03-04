# Guardrails

Guardrails are constraints that make wrong agent outputs visible, impossible, or automatically correctable. They are the primary quality mechanism in agentic engineering — not manual code review.

## Why Guardrails, Not Review

In Scrum, a developer might produce 50–200 lines of meaningful change per day. A human reviewer can keep up. In agentic workflows, an agent can produce 1000+ lines per session, across multiple files, refactoring across boundaries. The economics of manual review break down.

Guardrails shift the burden: instead of reviewing every output, you design a system where wrong outputs fail loudly.

## Categories

### Static Guardrails (before runtime)

Catch structural, stylistic, and security issues in code before it runs.

| Tool Type | Purpose | Examples |
|---|---|---|
| Linter | Style and correctness | ESLint, Ruff, golangci-lint |
| Type Checker | Type safety | TypeScript, mypy, pyright |
| SAST | Security vulnerabilities | Semgrep, CodeQL, Bandit |
| Dependency Scanner | Known CVEs in deps | Trivy, Snyk, Dependabot |
| Code Health Score | Complexity, duplication | SonarQube, Code Climate |

### Dynamic Guardrails (at runtime)

Catch behavioral issues that only appear when code executes.

| Tool Type | Purpose | Examples |
|---|---|---|
| Unit Tests | Component correctness | pytest, Jest, xUnit |
| Integration Tests | Component interaction | Testcontainers, REST clients |
| E2E Tests | Full system behavior | Playwright, Cypress |
| DAST | Security in running app | OWASP ZAP, Burp Suite |
| Mutation Testing | Test quality | Mutmut, Stryker, PIT |

### Semantic Guardrails (meaning and intent)

Catch cases where code is syntactically correct but semantically wrong.

| Tool Type | Purpose | Examples |
|---|---|---|
| Evals | LLM output quality | Custom eval harnesses, Promptfoo |
| Contract Tests | API behavior matches spec | Pact, Dredd |
| Business Logic Tests | Domain rules enforced | Domain-specific test suites |

## Designing Guardrails

Good guardrails have three properties:

1. **Automatic** — no human needs to trigger them; CI runs them on every commit
2. **Fast** — slow feedback loops invite workarounds; aim for <5 min for the critical path
3. **Actionable** — the failure message tells the agent (or developer) what to fix

Guardrails that are slow, flaky, or unclear get disabled. Disabled guardrails are worse than no guardrails — they create false confidence.

## Guardrails as Agent Feedback

In an agentic loop, guardrail output feeds back into the agent:

```
Agent generates code
  → CI runs guardrails
  → Failures returned to agent
  → Agent fixes and re-submits
  → Loop until green
```

This is why Code Health Scores and linter output need to be machine-readable and included in the agent's context. A human-readable HTML report helps developers; a structured JSON output helps agents.

## The Floor

At minimum, every agentic project needs:

- [ ] Linter (fast, zero-tolerance)
- [ ] Type checking (if typed language)
- [ ] Unit tests with coverage gate
- [ ] SAST scan
- [ ] Dependency vulnerability scan
- [ ] AGENTS.md documenting what "green" means

Everything above this is leverage.
