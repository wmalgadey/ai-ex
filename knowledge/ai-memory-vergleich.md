---
URL: https://github.com/mem0ai/mem0, https://github.com/supermemoryai/supermemory, https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/memory, https://github.com/campfirein/byterover-cli
Gespeichert: 2026-04-05
---

# AI Memory — Projekte im Vergleich

Vier Ansätze für persistentes Gedächtnis in KI-Agenten, gefunden im April 2026.

---

## mem0

**→ github.com/mem0ai/mem0** — Y Combinator S24, Apache 2.0

Universeller Memory-Layer für AI Agents. Speichert auf drei Ebenen: User, Session, Agent. Abruf per semantischer Suche, neue Fakten werden nach jeder Konversation extrahiert.

Technisch: LLM-basierte Extraktion (Default: GPT-4), mehrere Vector-Backends wählbar. Sowohl self-hosted (pip/npm) als auch Managed Service.

Eigene Benchmarks: 26% Accuracy-Verbesserung gegenüber OpenAI Memory, 91% schnellere Antworten, 90% weniger Token-Verbrauch.

---

## Supermemory

**→ github.com/supermemoryai/supermemory** — Benchmark-Führend

Memory- und Kontext-Layer mit Fokus auf externe Datenquellen. Verbindet sich mit Google Drive, Gmail, Notion, OneDrive, GitHub — Fakten werden kontinuierlich synchronisiert.

Highlights:
- Hybrid Search: RAG + personalisiertes Memory in einer Anfrage
- User Profiles: statische Fakten + dynamische Zusammenfassungen, ~50ms Abruf
- Multi-modal: PDF, Bild (OCR), Video (Transkription), Code

Externe Benchmarks: #1 auf LongMemEval (81.6%), LoCoMo, ConvoMem.

Verfügbar als App (app.supermemory.ai), MCP-Plugin für Claude/Cursor/VS Code, NPM/PyPI SDK.

---

## Vertex AI Memory Bank

**→ cloud.google.com/vertex-ai — Google Cloud, Managed**

Googles eigener verwalteter Memory-Service für Agenten. Keine eigene Vector-DB nötig — alles läuft in GCP, Daten bleiben im eigenen Projekt.

Mechanismus: Auto-Recall (relevante Memories vor jedem Turn per Similarity Search injiziert) + Auto-Capture (Fakten nach jeder Konversation extrahiert, dedupliziert, mit bestehenden Memories zusammengeführt).

Besonderheit: User-scoped Memory, d.h. Präferenzen aus einer Agent-Session sind in anderen Agents desselben Users verfügbar.

Preise: $0.25/1.000 Memories (Storage), $0.50/1.000 Retrievals (erste 1.000/Monat free), Gemini-Tokenkosten für Extraktion. Typisch für einen Einzelnutzer: ~$8/Monat.

Plugin für OpenClaw: [openclaw-vertexai-memorybank](https://github.com/Shubhamsaboo/openclaw-vertexai-memorybank)

---

## ByteRover CLI

**→ github.com/campfirein/byterover-cli** — Dev-fokussiert

CLI-Tool (`brv`) für persistentes Memory in Coding-Agenten. Erzeugt eine "Agentic Map" des Projekts — strukturiertes Wissen im Context-Tree, cloud-synchronisiert und team-fähig.

Unterstützt 20+ LLM-Provider, 24 eingebaute Agent-Tools (Code-Ausführung, File-Ops, Memory-Management), 22+ Integrationen (Cursor, Claude Code, Windsurf, Cline). MCP-kompatibel.

Benchmark: 96.1% auf Long-Context Retrieval.

Unterschied zu den anderen: kein User-Memory, sondern **Projekt-/Codebase-Memory** für Entwickler-Workflows.

---

## Einordnung

| Projekt | Fokus | Hosting | Besonderheit |
|---|---|---|---|
| mem0 | User/Agent Memory | Self-hosted + Managed | Breiteste LLM/Backend-Unterstützung |
| Supermemory | User Memory + externe Quellen | Managed (Cloud) | Beste externe Benchmarks, Connector-Ökosystem |
| Vertex AI Memory Bank | Agent Memory (GCP) | Google Managed | Multi-Agent-sharing, zero Infrastruktur |
| ByteRover CLI | Codebase/Projekt Memory | Self-hosted + Cloud Sync | Dev-Workflow, Team-Sharing |

## Einordnung im größeren Kontext

AI Memory (diese Tools) ist die Laufzeit-Ebene: automatisch, agent-seitig, flüchtig bis persistent.

Zwei verwandte Ansätze auf anderen Ebenen:
- [Karpathy: LLM Wiki](karpathy-llm-wiki.md) — kuratierter Wissensspeicher (Markdown-Wiki, menschlich/agent gepflegt); strukturierter als Session-Memory, aber manuell getrieben
- [Feedback Flywheel](../agentic-engineering/feedback-flywheel.md) — Team-Lernen als sozialer Prozess; Erkenntnisse aus KI-Interaktionen fließen in geteilte Artefakte (AGENTS.md, Playbooks)

```
Session-Memory (mem0/Supermemory)     ← automatisch, Laufzeit
       ↓
LLM Wiki (Karpathy)                   ← kuratiert, persistent
       ↓
Feedback Flywheel (Fowler/Garg)       ← sozial, organisational
```

_Rekonstruiert aus GitHub READMEs und Dokumentation, 2026-04-05._

#memory #agents #infrastruktur #vergleich #mem0 #supermemory #vertexai #byterover
