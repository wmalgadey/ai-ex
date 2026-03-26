# Rhizome — Semantische Backlinks für Obsidian

**Quelle:** https://github.com/matzalazar/rhizome
**Gespeichert:** 2026-03-26

CLI-Tool das automatisch `## Related Notes`-Sektionen mit `[[wikilinks]]` in Vault-Dateien schreibt — basierend auf semantischer Ähnlichkeit (Cosine Similarity über Embeddings), nicht auf Keyword-Matching.

> Instead of keyword matching, it uses cosine similarity over dense embeddings — so it catches semantic relationships even when notes don't share a single word.

**Technisch:**
- 100% lokal — ONNX Runtime auf CPU, kein GPU, kein Netzwerk nach erstem Modell-Download (~250 MB)
- Modell: `paraphrase-multilingual-MiniLM-L12-v2` — funktioniert für gemischtsprachige Vaults out of the box
- Kleines Vault: exaktes numpy-Search; großes Vault: approximiertes HNSW
- Idempotent — re-run ersetzt Section, keine Duplikate
- Dry-run Modus vor jedem Schreiben
- Timestamped Backups vor Änderungen

Kompatibel mit Obsidian und Logseq.

#obsidian #vault #semantic-search #embeddings #backlinks #local-first
