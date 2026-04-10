---
URL: https://claude.com/blog/the-advisor-strategy
Gespeichert: 2026-04-09
---

# The Advisor Strategy

_9. April 2026 — Claude Platform Blog_

> "Pair Opus as an advisor with Sonnet or Haiku as an executor, and get near Opus-level intelligence in your agents at a fraction of the cost."

## Konzept

Invertiert das klassische Orchestrator-Pattern:

- **Klassisch:** Großes Modell orchestriert, delegiert an kleine Worker
- **Advisor Strategy:** Kleines Modell (Sonnet/Haiku) fährt durch, eskaliert bei Bedarf an großes Modell (Opus)

Opus ruft keine Tools auf, produziert keinen User-Output — gibt nur einen Plan zurück. Der Executor macht weiter.

## Zahlen

- Sonnet + Opus Advisor vs. Sonnet solo: **+2.7 Punkte SWE-bench Multilingual, -11.9% Kosten**
- Haiku + Opus Advisor: BrowseComp 41.2% vs. 19.7% solo — bei 85% Kostenersparnis gegenüber Sonnet

## API

```python
response = client.messages.create(
    model="claude-sonnet-4-6",  # executor
    tools=[
        {
            "type": "advisor_20260301",
            "name": "advisor",
            "model": "claude-opus-4-6",
            "max_uses": 3,
        },
        # ... your other tools
    ],
    messages=[...]
)
```

- Beta-Header: `anthropic-beta: advisor-tool-2026-03-01`
- Advisor-Tokens werden separat im Usage-Block ausgewiesen
- `max_uses` begrenzt Advisor-Calls pro Request

## Links

- [Blog](https://claude.com/blog/the-advisor-strategy)
- [Docs](https://platform.claude.com/docs/en/agents-and-tools/tool-use/advisor-tool)

#anthropic #claude #advisor-strategy #cost-optimization #agentic #patterns
