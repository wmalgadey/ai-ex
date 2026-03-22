# Mastra — Observational Memory

**URL:** https://mastra.ai/docs/memory/observational-memory
**Gespeichert:** 2026-03-22

## Was ist das?

Mastra's Observational Memory (OM) ist ein Long-Context Memory-System für Agents. Zwei Hintergrund-Agents (Observer + Reflector) komprimieren die Konversationshistorie automatisch in "Observations" — damit bleibt der Kontext über lange Gespräche nutzbar ohne Token-Bloat.

## Wie es funktioniert

Drei Ebenen, angelehnt an menschliches Gedächtnis:

| Ebene | Inhalt | Trigger |
|---|---|---|
| **Recent Messages** | Aktuelle Nachrichten | immer |
| **Observations** | Komprimierte Fakten (wer sagte was, Entscheidungen, Kontext) | ab ~30.000 Token |
| **Reflections** | Hochrangige Synthese der Observations | ab ~40.000 Token in Observations |

Observer notiert Key Facts, Reflector synthetisiert Observations zu übergeordneten Mustern.

## Vorteile

- **Kompression**: Raw History komprimiert 5–40× in Observations
- **Prompt Caching**: Stabile Observation-Blöcke bleiben cacheable → Kostenreduktion
- **Noise-Reduktion**: Agents sehen relevante Info statt "noisy tool calls and irrelevant tokens"

## Konfiguration

```js
// Minimal
memory: { observationalMemory: true }  // nutzt Gemini 2.5 Flash by default

// Custom
memory: {
  observationalMemory: {
    model: myModel,
    observationThreshold: 30000,
    reflectionThreshold: 40000
  }
}
```

Unterstützte Storage-Adapter: PostgreSQL, LibSQL, MongoDB.

## Scopes

- **Thread scope** (default, stabil): Jeder Conversation-Thread hat eigene Observations
- **Resource scope** (experimentell): Observations spannen alle Threads eines Users → cross-conversation memory

## Retrieval Mode

Observations verlinken auf die Quell-Nachrichten. Agents können via `recall`-Tool auf den genauen Wortlaut zurückgreifen wenn die Zusammenfassung zu viel Detail verliert.

## Relevanz

Interessant als Referenz für NanoClaw/eigene Projekte: Das dreistufige Kompressionsmodell (Messages → Observations → Reflections) ist ein durchdachter Ansatz für Long-Term Memory der über einfaches CLAUDE.md-Schreiben hinausgeht.

## Tags

#memory #llm #mastra #agents #long-context #observational-memory #compression
