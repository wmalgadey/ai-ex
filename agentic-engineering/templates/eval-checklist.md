# Eval Coverage Checklist

Use this checklist when setting up or auditing eval coverage for an agentic project.

## Golden Dataset

- [ ] At least 20 representative (input, expected_output) pairs
- [ ] Edge cases covered (empty input, ambiguous input, boundary conditions)
- [ ] Failure cases covered (what the agent should *not* do)
- [ ] Dataset reviewed by a domain expert, not just the developer who wrote the prompts
- [ ] Dataset version-controlled alongside the code
- [ ] Last reviewed/updated: [date]

## Scorer Coverage

- [ ] Exact match scorer (for deterministic outputs)
- [ ] Semantic similarity scorer (for outputs where phrasing varies)
- [ ] Custom domain scorer for [domain-specific quality criteria]
- [ ] Regression detection (score delta vs. baseline, not just absolute score)

## CI Integration

- [ ] Evals run on every PR (or at minimum: on main branch merges)
- [ ] Score threshold defined and enforced (build fails below threshold)
- [ ] Eval results stored/logged (for trend analysis)
- [ ] Alert on significant score regression (>5% drop)

## Behavior Coverage

- [ ] Happy path: does it do the right thing on normal input?
- [ ] Edge cases: does it handle unusual but valid input?
- [ ] Refusal behavior: does it refuse insecure / out-of-scope requests?
- [ ] Convention adherence: does it follow AGENTS.md conventions?
- [ ] Ambiguity handling: does it ask when unclear, rather than guess?

## Regression Set

- [ ] Every bug found in production has a corresponding eval case
- [ ] Every model/prompt update triggers full regression eval run
- [ ] Baseline scores documented for current model version

## Documentation

- [ ] `evals/README.md` explains what's being evaluated and why
- [ ] Each eval case includes a comment explaining what it tests
- [ ] Scoring thresholds are justified (not arbitrary)
