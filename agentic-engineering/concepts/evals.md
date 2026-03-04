# Evals

Evals (evaluations) are systematic tests for LLM-generated output. They answer: "Is the output actually correct?" — not just "Does it compile and pass tests?"

Traditional tests verify that code behaves as specified. Evals verify that the specification itself was interpreted correctly, and that the agent's reasoning was sound.

## Why Evals Are Different From Tests

| Dimension | Tests | Evals |
|---|---|---|
| What they check | Code behavior | LLM output quality + correctness |
| Determinism | Fully deterministic | Often probabilistic |
| Pass criteria | Binary (pass/fail) | Often graded (0–1 score) |
| Who writes them | Developers | Developers + domain experts |
| When they matter | Always | Critical for agentic workflows |

## Types of Evals

### 1. Correctness Evals
Does the output match the expected answer?

```python
# Example: Did the agent generate correct SQL?
result = agent.generate_sql("customers who bought in last 30 days")
assert result == expected_sql  # or: assert semantic_equivalence(result, expected_sql)
```

### 2. Behavior Evals
Does the agent behave correctly in edge cases?

- Does it refuse to generate insecure code?
- Does it follow the AGENTS.md conventions?
- Does it handle ambiguous requirements by asking, not guessing?

### 3. Regression Evals
Did a model or prompt change break previously working behavior?

Maintain a golden dataset of (input, expected_output) pairs. Run on every model or prompt update.

### 4. Robustness Evals
Does the output quality hold under variation?

- Paraphrase the same request 5 ways — does the agent produce equivalent output?
- Introduce noise in the input — does quality degrade gracefully?

## Building an Eval Harness

Minimal viable eval setup:

```
evals/
├── datasets/
│   ├── golden-set.jsonl       # (input, expected_output) pairs
│   └── edge-cases.jsonl
├── scorers/
│   ├── exact_match.py
│   ├── semantic_similarity.py
│   └── custom_domain_scorer.py
├── run_evals.py               # Entry point
└── README.md                  # What's being evaluated and why
```

### The JSONL Format

```jsonl
{"input": "Generate a function that...", "expected": "def foo(x):", "tags": ["python", "functions"]}
{"input": "Refactor this to use...", "expected": "...", "tags": ["refactoring"]}
```

## Evals in CI

Evals belong in CI — at minimum on main branch, ideally on every PR.

```yaml
# .github/workflows/evals.yml (example)
- name: Run evals
  run: python evals/run_evals.py --threshold 0.85
  # Fail the build if eval score drops below threshold
```

Gate on *score regression*, not absolute score. A new feature might lower aggregate score if it adds hard cases — that's acceptable. A model update that breaks existing behavior is not.

## The Domain Expert Problem

The hardest part of evals is the golden dataset. It requires domain expertise to know what "correct" looks like. This is why Florian Burka identifies domain expertise as one of the four key levers — not intelligence, but knowledge of what correct means in your specific context.

Invest time here. An eval harness with a weak golden set gives false confidence. An eval harness with a strong golden set is a force multiplier.

## See Also

- `../templates/eval-checklist.md` — checklist for eval coverage
- Tools: [Promptfoo](https://promptfoo.dev), [LangSmith](https://smith.langchain.com), [RAGAS](https://ragas.io)
