# Agent Contracts: AGENTS.md + OpenAPI

In agentic engineering, contracts are not just for humans. They are the primary interface between agent and codebase. A well-written contract is the single highest-leverage investment you can make.

## AGENTS.md

`AGENTS.md` lives in the root of every repo. It tells an agent:

- **What this repo does** — scope and purpose
- **How to work here** — conventions, patterns, constraints
- **What not to touch** — protected files, generated code, infra boundaries
- **How to verify correctness** — which tests to run, what "done" means
- **Who to consider** — downstream consumers, API contracts

### Why It Matters

Without `AGENTS.md`, every agent session starts from zero. The agent reads the code, infers conventions, and sometimes gets them wrong. With it, you encode your domain knowledge once and it applies to every agent run.

Think of it as a README written for an agent that can read code but doesn't know *why* it was written that way.

### What Goes In It

```markdown
# AGENTS.md

## Purpose
[What this repo does in 2-3 sentences]

## Key Conventions
- [Language/framework version]
- [File naming conventions]
- [Import style]
- [Error handling patterns]

## Architecture
- [High-level component overview]
- [Key abstractions and their roles]

## Working with this Repo
- Run tests: `[command]`
- Build: `[command]`
- Lint: `[command]`

## Do Not Modify
- [Generated files]
- [Pinned versions or configs]

## Definition of Done
- [ ] All tests pass
- [ ] Lint clean
- [ ] No new security findings
- [ ] [Domain-specific checks]
```

See `../templates/AGENTS.md` for a full template.

---

## OpenAPI Specs

OpenAPI specs serve as machine-readable contracts for APIs. In an agentic context:

- Agents use them to understand what an API does *without reading implementation*
- They constrain what an agent can generate (schema validation)
- They enable DAST tools to test the actual API against the spec automatically

### Agentic Benefits

| Without OpenAPI | With OpenAPI |
|---|---|
| Agent reads source to infer API shape | Agent reads spec — deterministic, version-controlled |
| No automatic drift detection | CI fails if implementation diverges from spec |
| DAST has no contract to test against | DAST validates every endpoint against the spec |

### Minimal Viable Spec

Even a partial spec is better than none. Start with the endpoints agents will most likely call or modify. Expand as you go.

---

## Contracts as Feedback Loops

The real power: contracts don't just inform agents — they constrain them. An agent that generates code violating the OpenAPI spec gets caught immediately by the CI pipeline. Linter scores, test failures, and spec violations all become automatic signals the agent can act on.

This is the "Linter und Code Health Scores werden zum automatischen Feedback-Loop direkt in den Agent zurück" principle. The agent doesn't need a human reviewer for every change — it needs a system that makes wrong outputs visible.
