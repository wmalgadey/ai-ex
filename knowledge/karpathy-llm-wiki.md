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
- **qmd** ([github.com/tobi/qmd](https://github.com/tobi/qmd)) für lokale Wiki-Suche

### qmd

On-device Suchmaschine für Markdown-Notizen und Wissensdatenbanken. Drei Modi:

1. `search` — BM25 Full-Text
2. `vsearch` — Vector/Semantisch
3. `query` — Hybrid + LLM-Reranking (beste Qualität)

Kein externer API-Call, keine Daten verlassen das System. Output in JSON für LLM-Consumption optimiert, MCP-Server-Modus für Claude Desktop verfügbar.

Passt als Query-Layer direkt in den LLM-Wiki-Workflow: LLM ruft `query` auf, bekommt strukturierte Ergebnisse, entscheidet welche Wiki-Seiten relevant sind.

### llm-wiki-compiler — Direkte Implementierung

**→ [github.com/atomicmemory/llm-wiki-compiler](https://github.com/atomicmemory/llm-wiki-compiler)** — MIT, TypeScript, Node ≥18

Implementiert Karpathys Pattern direkt als CLI. Zwei-Phasen-Pipeline: erst Konzept-Extraktion aus allen Quellen, dann Wiki-Generierung. SHA-256-Hashing für inkrementelles Processing — nur geänderte Quellen lösen LLM-Calls aus.

Befehle entsprechen exakt den drei Operationen:

| Befehl | Karpathy-Operation |
|---|---|
| `ingest` | Ingest |
| `compile` | Ingest (Verarbeitung) |
| `query` | Query |
| `lint` | Lint |
| `watch` | Automatisches Re-Compile |

Output-Struktur:
```
wiki/
├── concepts/   (ein .md pro Konzept, YAML-Frontmatter)
├── queries/    (gespeicherte Antworten, indiziert)
└── index.md    (auto-generiert)
```

Obsidian-kompatibel mit `[[wikilink]]`-Support. `--save`-Flag speichert Query-Antworten als neue Wiki-Seiten — Wissen akkumuliert sich über Zeit. Paragraph-Level-Attribution mit `^[filename.md]`-Markern.

Aktuell: Anthropic-only, optimiert für kleine Corpora (Dutzende Quellen). Roadmap: Multi-Provider, Semantic Search, MCP-Server.

### Graphify — Visualisierungsschicht

**→ [github.com/safishamsi/graphify](https://github.com/safishamsi/graphify)** — MIT

Ergänzung zu qmd: wo qmd text-basiert sucht, macht Graphify Beziehungen sichtbar. Verwandelt Ordner mit Code, Dokumentation, Papers und Bildern in interaktive Knowledge-Graphen.

Zwei Verarbeitungs-Passes:
1. **Deterministisch:** AST-Extraktion via tree-sitter — Klassen, Funktionen, Call-Graphs (kein LLM-Overhead)
2. **LLM-parallel:** Claude Subagents extrahieren Konzepte und Beziehungen aus Non-Code-Dateien

Ergebnis: NetworkX-Graph, Leiden Community Detection, Export als HTML / JSON / Markdown-Wiki. Neo4j-Export optional.

Relationship-Typen: `EXTRACTED` (sicher), `INFERRED` (mit Confidence-Score), `AMBIGUOUS`.

Trigger via `/graphify` in Claude Code, Codex, OpenClaw. Behaupteter Effizienz-Wert: 71,5× weniger Token pro Query gegenüber Raw-File-Lesen (bei großen Mixed-Corpora).

**Passt in den LLM-Wiki-Stack als Visualisierungsschicht:**
```
Raw Sources → Wiki (Karpathy/LLM) → Graph (Graphify) → Query (qmd)
```

## Was bereits existiert

**ai-ex ist bereits eine LLM Wiki.** Marvin pflegt sie aktiv: Artikel werden beim Ingest extrahiert, in thematische MOCs eingetragen, cross-referenziert. Das Muster ist identisch — ohne dass Karpathys Post der Ausgangspunkt war.

**Im Zettelkasten** gibt es bereits:
- `2025-12-05_2155 - LLM Council` — früheres Karpathy-Projekt (Multi-LLM-Voting)
- `Agentic Engineering MOC.md` — verlinkt Vibe Coding als Kontrastpunkt; LangGraph als graph-basierte Orchestrierung
- `2025-12-18_1002 - Spec-Driven Development` — verwandt (Struktur vs. Improvisation)
- `Personal Knowledge Management MOC.md` — Backlinks, bidirektionale Verlinkung (konzeptueller Vorläufer zu Graphify)
- `Claude Code Workflow für Zettelkasten.md` — Backlink-Management, visueller Graph-Überblick als explizites Ziel
- `PostgreSQL als Graph-Datenbank mit pgRouting` — Graph-Konzept bereits bekannt, anderer Stack

**Verwandt im ai-ex — drei Ebenen desselben Stacks:**

```
Session-Memory (mem0/Supermemory)     ← automatisch, Laufzeit
       ↓
LLM Wiki (Karpathy) ← hier           ← kuratiert, persistent
       ↓
Feedback Flywheel (Fowler/Garg)       ← sozial, organisational
```

- [AI Memory Vergleich](ai-memory-vergleich.md) — Ebene darunter: automatische Laufzeit-Memory (mem0, Supermemory etc.), User-/Session-scoped
- [Feedback Flywheel](../agentic-engineering/feedback-flywheel.md) — Ebene darüber: wie Teams kollektiv lernen und Artefakte befüllen; der menschliche Ingest-Loop für die Wiki
- [Semantic Contracts](../agentic-engineering/semantic-contracts.md) — CLAUDE.md als Schema-Datei
- [Rhizome — Semantische Backlinks für Obsidian](werkzeuge-und-infrastruktur.md) — ähnlicher Ansatz: semantische Verlinkung für Markdown-Vaults; Graphify geht weiter (Code + Docs + Bilder, interaktiv)

## NanoClaw

Ein Skill für das LLM-Wiki-Pattern ist für ein kommendes Update geplant.

_Rekonstruiert aus dem Karpathy-Gist und X-Thread, 2026-04-06. Graphify ergänzt 2026-04-07. llm-wiki-compiler ergänzt 2026-04-08._

#karpathy #llm-wiki #knowledge-management #rag #obsidian #memory #graphify #knowledge-graph #llm-wiki-compiler
