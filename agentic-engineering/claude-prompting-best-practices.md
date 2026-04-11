---
URL: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices
Gespeichert: 2026-04-11
---

# Claude Prompting Best Practices (Anthropic, Claude 4.x)

Offizielle Anthropic-Referenz für Prompt Engineering mit Claude Opus 4.6, Sonnet 4.6, Haiku 4.5. Volltext unter obiger URL. Hier: die nicht-offensichtlichen Punkte.

---

## Allgemeine Prinzipien

**"Brilliant but new employee"** — Claude kennt keine Konventionen des Teams. Je präziser die Anweisung, desto besser das Ergebnis.

**Golden Rule:** Prompt einer Kollegin zeigen die keinen Kontext hat. Wenn sie verwirrt wäre, wird Claude es auch sein.

**Kontext + Begründung > bloße Regel:**
```
Schlecht:  "NEVER use ellipses"
Besser:    "Never use ellipses — the output will be read aloud by TTS"
```
Claude ist intelligent genug, aus der Begründung zu generalisieren.

**Few-Shot:** 3–5 Beispiele in `<example>` / `<examples>` Tags. Divers, randfall-abdeckend. Claude kann bestehende Beispiele auf Relevanz und Diversität prüfen.

**XML-Tags** für komplexe Prompts mit gemischtem Inhalt (Instruktionen + Kontext + Beispiele + Input). Konsistente, beschreibende Tag-Namen. Hierarchisch schachteln wenn sinnvoll.

---

## Long Context

- **Dokumente an den Anfang, Query ans Ende** — kann Performance bis 30% verbessern bei komplexen Multi-Dokument-Inputs
- Dokumente in `<document index="n"><source>...</source><document_content>...</document_content></document>` wrappen
- **Quote first:** Claude anweisen, erst relevante Zitate zu extrahieren, dann zu antworten — filtert Noise aus langen Dokumenten

---

## Output & Formatting

Claude 4.x ist standardmäßig prägnanter und direkter als frühere Modelle. Kann nach Tool-Calls ohne Summary zum nächsten Schritt springen.

**Format steuern:**
- Statt "Do not use markdown" → "Write in smoothly flowing prose paragraphs"
- XML-Format-Indikator: "Write prose in `<smoothly_flowing_prose_paragraphs>` tags"
- Prompt-Stil beeinflusst Output-Stil — Markdown im Prompt → mehr Markdown im Output

**Prefill deprecated:** Ab Claude 4.6 wird Prefill auf dem letzten Assistant-Turn nicht mehr unterstützt. Mythos Preview wirft 400-Fehler. Migration:
- Format-Erzwingung → Structured Outputs
- Preamble unterdrücken → "Respond directly without preamble. Do not start with 'Here is...', 'Based on...'"
- Fortsetzungen → In User-Turn verschieben: "Your previous response was interrupted ending with `[text]`. Continue."

---

## Tool Use

**Explizit fordern, nicht implizieren:**
```
Schlecht:  "Can you suggest some changes?"   → Claude schlägt vor statt zu ändern
Besser:    "Change this function to improve performance."
```

**Parallele Tool-Calls (~100% mit explizitem Prompt):**
```
If you intend to call multiple tools and there are no dependencies between the tool
calls, make all of the independent tool calls in parallel. Never use placeholders
or guess missing parameters in tool calls.
```

**Claude Opus 4.6:** Aggressive Subagent-Nutzung — kann für simple Aufgaben unnötige Subagents spawnen. Gegenmittel:
```
Use subagents when tasks can run in parallel, require isolated context, or involve
independent workstreams. For simple tasks, sequential operations, or single-file
edits, work directly.
```

---

## Thinking / Reasoning

**Adaptive Thinking** (Claude 4.6) ersetzt Extended Thinking mit `budget_tokens` (deprecated):
```python
# Vorher (deprecated)
thinking={"type": "enabled", "budget_tokens": 32000}

# Nachher
thinking={"type": "adaptive"},
output_config={"effort": "high"}  # oder max/medium/low
```

`effort`-Parameter steuert Denk-Tiefe. Claude kalibriert selbst wie viel es denkt.

**Overthinking:** Claude Opus 4.6 neigt zu extensiver Vorab-Exploration. Gegenmittel:
- Aggressive Prompts (CRITICAL: MUST use...) → normale Formulierungen
- `effort` auf niedrigere Stufe setzen
- Explizit: "Choose an approach and commit to it. Avoid revisiting unless new information contradicts your reasoning."

**Multishot mit Thinking:** `<thinking>`-Tags in Few-Shot-Beispielen zeigen das gewünschte Reasoning-Muster.

---

## Agentic Systems

**Reversibilität vor Aktion:**
```
Consider the reversibility and potential impact of your actions. For actions that
are hard to reverse, affect shared systems, or could be destructive, ask the user
before proceeding.

Examples requiring confirmation: rm -rf, git push --force, git reset --hard,
force-push, posting to external services.
```

**State Management:**
- Strukturierte Formate (JSON) für Tests/Task-Status
- Freitext für Fortschrittsnotizen
- Git als State-Log über mehrere Sessions

**Anti-Overengineering:**
```
Only make changes that are directly requested or clearly necessary.
Don't add features, refactor code, or make "improvements" beyond what was asked.
Don't add docstrings/comments to code you didn't change.
Don't create helpers for one-time operations.
```

**Anti-Halluzination:**
```
<investigate_before_answering>
Never speculate about code you have not opened. If the user references a specific
file, you MUST read the file before answering.
</investigate_before_answering>
```

**Context Awareness:** Claude 4.6 trackt verbleibendes Token-Budget und kann Context-Compaction antizipieren.

---

## Sonnet 4.6 Migration von 4.5

- Default `effort`: **high** (Sonnet 4.5 hatte kein effort-Param) → explizit auf `medium` oder `low` setzen für Latenz-sensitive Workloads
- Empfehlung: `max_tokens=64000` bei medium/high effort
- Für Chat/Klassifizierung: `effort: low`, thinking disabled

_Aus Anthropic Docs, 2026-04-11._

#claude #prompting #best-practices #agentic #api #anthropic
