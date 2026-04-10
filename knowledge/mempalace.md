---
URL: https://github.com/milla-jovovich/mempalace
Gespeichert: 2026-04-10
---

# MemPalace — Lokale AI Memory mit Palace-Metapher

Open-Source AI Memory System. Lokale Speicherung ohne Cloud-Abhängigkeit. Philosophie: "store everything, then make it findable" — statt LLM-seitiger Zusammenfassung alles verbatim behalten und besser durchsuchbar machen.

## Architektur: The Palace

Inspiriert von antiken Gedächtnistechniken (Method of Loci):

| Ebene | Bedeutung |
|---|---|
| **Wings** | Projekte oder Personen (Domänen) |
| **Rooms** | Topics innerhalb einer Wing (z.B. "auth", "billing") |
| **Halls** | Memory-Typen (facts, events, discoveries, preferences, advice) |
| **Closets** | Zusammenfassungen → zeigen auf Original |
| **Drawers** | Verbatim-Originaldateien |
| **Tunnels** | Cross-References zwischen Wings zum selben Thema |

## Stack

ChromaDB (Vector) + SQLite (Knowledge Graph), Python 3.9+, MIT.

Läuft als CLI, MCP-Server (Claude, ChatGPT, Cursor, Gemini), Python-Library, Claude Code Plugin. Vollständig lokal, kostenlos.

## Behauptete Benchmarks

- **96.6% R@5 auf LongMemEval** — Raw-Verbatim-Modus, 500 Testfragen, kein API-Call
- **+34% Retrieval-Verbesserung** durch Palace-Struktur gegenüber ungefilterten Suchen
- **AAAK-Modus**: 84.2% (komprimiert, verlustbehaftet)

## Issue #27 — Kritische Diskrepanzanalyse

[github.com/milla-jovovich/mempalace/issues/27](https://github.com/milla-jovovich/mempalace/issues/27) — 199 Upvotes, 36 Kommentare

Entwickler lhl dokumentiert erhebliche Abweichungen zwischen README-Behauptungen und tatsächlicher Implementierung:

**Contradiction Detection:** README bewirbt automatische Widerspruchserkennung — Code blockt nur identische Tripel. Widersprüchliche Fakten akkumulieren stillschweigend.

**Komprimierung:** "30x Komprimierung, zero information loss" — AAAK ist nachweislich verlustbehaftet, 12.4pp Rückgang im Benchmark.

**Benchmark-Attribution:** Die 96.6% kommen von ChromaDB + Standard-Embeddings mit Raw-Text. Die Palace-Struktur (Wings/Rooms/Halls) ist nicht am Benchmark beteiligt — er misst das Embedding-Modell, nicht die MemPalace-Architektur.

**+34% Boost:** Entspricht Standard-Metadaten-Filterung in jeder Vektor-Datenbank — keine neuartige Retrieval-Mechanik.

**Community-Urteil:** "Readme-Driven Development" — README priorisiert Marketing über Implementierung.

## Einordnung

MemPalace als Konzept ist interessant: Palace-Metapher als Organisationsprinzip, verbatim statt Zusammenfassung. Die Implementierung hält (noch) nicht, was das README verspricht.

Besonders relevant als Warnung: **hohe Benchmarkzahlen im Memory-Bereich sorgfältig prüfen** — der 96.6%-Score misst das Embedding-Modell, nicht das System.

Verwandt:
- [AI Memory — Projekte im Vergleich](ai-memory-vergleich.md) — andere Memory-Systeme (mem0, Supermemory, Vertex AI)
- [llm-memory.org](llm-memory-org.md) — Community-Vergleichsplattform mit 19 Tools

_Rekonstruiert aus GitHub README und Issue #27, 2026-04-10._

#memory #agents #vergleich #benchmark #kritik #mempalace
