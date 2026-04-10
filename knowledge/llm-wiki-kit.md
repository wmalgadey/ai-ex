---
URL: https://github.com/SantiagoBobrik/llm-wiki-kit
Gespeichert: 2026-04-10
---

# llm-wiki-kit — Claude Code Plugin für Karpathy-style Wiki

Claude Code Plugin das einen Obsidian-Vault in eine selbst-pflegende Wissensbasis verwandelt. Direkter Nachfolger von Karpathys LLM-Wiki-Pattern, implementiert als Skills.

## Fünf Operationen

| Befehl | Funktion |
|---|---|
| `init` | Vault-Struktur + Wiki-Regeln bootstrappen |
| `compile` | Raw-Clippings einlesen, nach Thema gruppieren, zu Wiki-Artikeln synthetisieren |
| `search` | Wiki abfragen, zitierte Antworten zurückgeben |
| `save` | Erkenntnisse aus Konversation zurück in die Wiki speichern |
| `lint` | Widersprüche, Lücken, unbelegte Aussagen, Ton auditieren |

## Drei Schichten

```
Raw/   — unveränderliche Quell-Clippings (via Obsidian Web Clipper)
Wiki/  — synthetisierte, verlinkte Artikel (Claude pflegt)
CLAUDE.md — Vertrag: Struktur, Frontmatter, Schreibregeln, Ton
```

Claude liest den Vertrag automatisch da er im Projekt-Kontext liegt.

## Einordnung

Direkter Nachfolger von [Karpathy: LLM Wiki](karpathy-llm-wiki.md) — operationalisiert durch Claude Code Skills + Obsidian. Nutzt Obsidian CLI für programmatische Vault-Operationen.

Vergleich mit [llm-wiki-compiler](karpathy-llm-wiki.md#llm-wiki-compiler--direkte-implementierung): Compiler ist TypeScript-CLI für beliebige Quellen, llm-wiki-kit ist Obsidian-nativer Claude-Code-Skill. MIT.

_Aus GitHub README, 2026-04-10._

#llm-wiki #obsidian #claude-code #knowledge-management #karpathy
