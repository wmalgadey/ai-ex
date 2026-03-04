# AGENTS.md

> This file is a contract for AI agents working in this repository.
> It defines scope, conventions, constraints, and the definition of done.
> Keep it accurate. An outdated AGENTS.md is worse than none.

---

## Purpose

<!-- 2–3 sentences: what does this repo do and why does it exist? -->
[Describe the repository purpose here]

## Technology Stack

- **Language:** [e.g. Python 3.12, TypeScript 5.x, Go 1.22]
- **Framework:** [e.g. FastAPI, Next.js, Gin]
- **Key dependencies:** [list 3–5 most important]
- **Database:** [if applicable]

## Repository Structure

```
[repo-name]/
├── src/           # [what lives here]
├── tests/         # [test structure]
├── docs/          # [documentation]
└── [other dirs]   # [description]
```

## Key Conventions

### Code Style
- [Formatter and config, e.g. "Black, configured in pyproject.toml"]
- [Linter and rules, e.g. "Ruff, no-unused-imports enforced"]
- [Naming conventions]

### Architecture Patterns
- [Key patterns used, e.g. "Repository pattern for data access"]
- [Error handling approach]
- [Logging conventions]

### Testing Conventions
- [Test file naming, e.g. "test_*.py alongside source files"]
- [Test naming, e.g. "test_[what]_[condition]_[expected]"]
- [Fixture conventions]

## Development Workflow

```bash
# Setup
[setup command]

# Run tests
[test command]

# Lint
[lint command]

# Build
[build command]

# Run locally
[run command]
```

## Do Not Modify Without Explicit Instruction

- `[generated files — e.g. migrations/, generated/]`
- `[pinned configurations]`
- `[shared infrastructure files]`

## External Contracts

<!-- APIs and services this repo depends on or exposes -->
- **Exposes:** [OpenAPI spec location, if applicable]
- **Consumes:** [External APIs or services]

## Definition of Done

A change is complete when:

- [ ] All existing tests pass (`[test command]`)
- [ ] New behavior has test coverage
- [ ] Linter passes with zero warnings (`[lint command]`)
- [ ] No new SAST findings (`[sast command if applicable]`)
- [ ] AGENTS.md updated if conventions changed
- [ ] [Domain-specific checks]

## Known Gotchas

<!-- Things that trip up agents (and new developers) -->
- [e.g. "The `config/` directory is env-specific — never hardcode values"]
- [e.g. "All DB queries go through the repository layer, never direct SQL in handlers"]

## Context for Agents

<!-- Anything else an agent needs to know to work effectively here -->
- **Preferred approach for [common task]:** [description]
- **When in doubt:** [what should an agent do — ask, or make a conservative choice?]
