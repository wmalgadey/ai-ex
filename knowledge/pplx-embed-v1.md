# Perplexity pplx-embed-v1 — Embedding Models

**Quelle:** https://the-decoder.de/perplexity-veroeffentlicht-speicherschonende-embedding-modelle-als-open-source/
**Datum:** 2026-02-28
**Lizenz:** MIT

## Modelle

- `pplx-embed-v1` — klassisches dichtes Text-Retrieval
- `pplx-embed-context-v1` — kontextuelles Embedding (umgebender Dokument-Kontext wird eingebettet, gut für mehrdeutige Passagen)
- Jeweils in **0.6B** und **4B** Parameter verfügbar

## Was sie besonders macht

- **Bidirektional:** Basiert auf Qwen3, aber umgebaut wie BERT — versteht Kontext in beide Richtungen (nicht nur links→rechts)
- **INT8-Quantisierung** nativ trainiert → 4× weniger Speicher ohne Qualitätsverlust
- **Binary-Variante:** 32× weniger Speicher, unter 1.6% Qualitätsverlust beim 4B-Modell
- **Kein Prefix-Prompt nötig** — viele Konkurrenten brauchen das, was zu Inkonsistenzen zwischen Indexierung und Query führt
- Trainiert auf ~250 Mrd. Token in 30 Sprachen

## Performance

| Benchmark | pplx-embed-v1-4B | Qwen3-Embedding-4B | gemini-embedding-001 |
|---|---|---|---|
| MTEB Retrieval (nDCG@10) | **69.66%** | 69.60% | 67.71% |
| ConTEB (kontextuell) | **81.96%** | — | — |

- Interner PPLXQuery2Query: 73.5% vs. 67.9% (Qwen3-4B)
- Das **0.6B-Modell** schlägt Qwen3-Embedding-4B in 3 von 5 RAG-Aufgaben (BERGEN-Benchmark)

## Verfügbarkeit

- HuggingFace: https://huggingface.co/collections/perplexity-ai/pplx-embed
- Perplexity API
- Frameworks: Transformers, SentenceTransformers, ONNX

## Use Case Einschätzung

Interessant für:
- **Lokale RAG-Pipelines** (Homelab) — kleines 0.6B-Modell sehr effizient
- **Multilingual Retrieval** (30 Sprachen)
- **Web-Scale Search** — speziell für große Dokumentkorpora optimiert
- Kontextuelles Modell für Wikis/Docs wo Passagen mehrdeutig sein können
