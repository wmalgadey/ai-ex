---
URL: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
Gespeichert: 2026-04-06
---

# Karpathy: LLM Wiki

April 2026 viral auf X — Andrej Karpathy beschreibt ein Wissensmanagementsystem, das er "LLM Wiki" nennt. Alternative zu RAG.

## Kernidee

Statt Dokumente für spätere Abfrage zu speichern (RAG), pflegt ein LLM eine persistent strukturierte Wiki. Drei Schichten:

```
Raw Sources  →  Wiki (LLM-geschrieben)  →  Schema (CLAUDE.md/AGENTS.md)
(unveränderlich)   (Markdown-Dateien)       (LLM-Verhalten konfiguriert)
```

Das LLM liest eine neue Quelle nicht einfach zur späteren Abfrage — es liest, extrahiert Schlüsselinformationen und integriert sie in die bestehende Wiki. Aktualisiert Entity-Seiten, revidiert Topic-Zusammenfassungen, anstatt jedes Mal von Grund auf neu zu kompilieren.

## Drei Operationen

**Ingest:** Neue Quelle hinzufügen → LLM diskutiert Erkenntnisse → aktualisiert 10–15 Wiki-Seiten gleichzeitig.

**Query:** Fragen gegen die Wiki → LLM durchsucht relevante Seiten → gute Antworten werden als neue Seiten eingefügt.

**Lint:** Periodische Prüfungen auf Widersprüche, verwaiste Seiten, fehlende Cross-References.

## Zwei spezielle Dateien

- `index.md` — Katalog aller Wiki-Seiten mit Zusammenfassungen
- `log.md` — Append-only-Journal aller Ingests und Queries

## Werkzeuge im Original-Stack

- Obsidian Web Clipper für schnelle Erfassung
- Obsidian Graph View zur Visualisierung
- `qmd` für lokale Wiki-Suche

## Was bereits existiert

**ai-ex ist bereits eine LLM Wiki.** Marvin pflegt sie aktiv: Artikel werden beim Ingest extrahiert, in thematische MOCs eingetragen, cross-referenziert. Das Muster ist identisch — ohne dass Karpathys Post der Ausgangspunkt war.

**Im Zettelkasten** gibt es bereits:
- `2025-12-05_2155 - LLM Council` — früheres Karpathy-Projekt (Multi-LLM-Voting)
- `Agentic Engineering MOC.md` — verlinkt Vibe Coding als Kontrastpunkt
- `2025-12-18_1002 - Spec-Driven Development` — verwandt (Struktur vs. Improvisation)

**Verwandt im ai-ex:**
- [AI Memory Vergleich](ai-memory-vergleich.md) — mem0, Supermemory etc. lösen das Memory-Problem anders (User-scoped, Session-scoped)
- [Semantic Contracts](../agentic-engineering/semantic-contracts.md) — CLAUDE.md als Schema-Datei

## NanoClaw

Ein Skill für das LLM-Wiki-Pattern ist für ein kommendes Update geplant.

_Rekonstruiert aus dem Karpathy-Gist und X-Thread, 2026-04-06._

#karpathy #llm-wiki #knowledge-management #rag #obsidian #memory
