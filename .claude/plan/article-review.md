# Article Review Plan
_Generated: 2026-03-22_
_Implemented: 2026-03-22_

## Zusammenfassung
22 files OK, 18 files need changes (plan listed 26 total files with issues)

## Dateien — Kein Handlungsbedarf

- `knowledge/clawclones.md` — kurz, sachlich, Tags vorhanden, Quelle angegeben
- `knowledge/llm-daydreaming-gwern.md` — KI-Marker vorhanden, Tags vorhanden, sachlich
- `knowledge/mastra-observational-memory.md` — kompakt, gut strukturiert, Tags vorhanden
- `knowledge/mcs-managed-claude-stack.md` — dicht und sachlich, Tags vorhanden
- `knowledge/romilly-claude-code-helpers.md` — kurz, Tags vorhanden, sinnvoll verlinkt
- `journal/openclaw-to-nanoclaw-journey.md` — Chronisten-Perspektive eingehalten, KI-Marker gesetzt, Tags vorhanden
- `agentic-engineering/concepts/guardrails.md` — sachlich, keine Dramatisierung, keine überflüssigen Zusammenfassungen
- `agentic-engineering/concepts/evals.md` — sachlich, gut strukturiert, keine Redundanz
- `agentic-engineering/templates/AGENTS.md` — Template, kein Artikel; Stilregeln nicht anwendbar
- `agentic-engineering/templates/eval-checklist.md` — Checkliste, kein Artikel; Stilregeln nicht anwendbar
- `agentic-engineering/resources/links.md` — reine Linkliste, passt
- `skills-and-agent/k8s-operator-dev/readme.md` — kompakt, sachlich
- `skills-and-agent/elephant-slices/user-story-writer/user-story-writer.md` — Agent-Definition (Frontmatter), kein Artikel

## Dateien — Anpassung nötig

### `knowledge/ai-bugfixing-workflow.md`
- [x] Kein Tags-Block am Ende — fehlt komplett.
- [ ] Workflow-Phasen sind paraphrasiert, nicht aus dem Original zitiert; direktere Auszüge wären laut Style Guide vorzuziehen.

### `knowledge/alistair-cockburn-hexagonal-claude.md`
- [x] Tags-Abschnitt steht in der Mitte des Dokuments, nicht am Ende — muss ans Ende verschoben werden.
- [ ] Abschnitt "Verwandte Ressourcen" enthält duplizierten Inhalt zu `romilly-claude-code-helpers.md`; wäre besser als reiner Link statt ausführlicher Inhaltswiedergabe.
- [x] "Was ist das?" + "Interessant für:"-Zeile formuliert explizit, warum es interessant ist — verstößt gegen Chronisten-Perspektive (kein "was man daraus lernen soll").
- [x] "Notizen"-Abschnitt ganz unten passt nicht zur Struktur; besser in Frontmatter oder weg.

### `knowledge/anthropic-courses.md`
- [x] Keine Tags am Ende.
- [ ] Kein Datum/Gespeichert-Eintrag. (Datum unbekannt — nicht hinzugefügt)
- [ ] Keine Quelle als Frontmatter-Block, nur URL-Zeile ohne Label — inkonsistent mit Konvention. (konservativ belassen)

### `knowledge/bmad-method.md`
- [ ] Slogans direkt aus dem Repo zitiert ("Breakthrough Method..."), aber nicht als Blockquote ausgewiesen — bereits als Blockquote in der Datei vorhanden.
- [ ] "100% free & open source. Keine Paywalls." — konservativ belassen.
- [x] Kein Tags-Block am Ende.

### `knowledge/claude-code-best-practice.md`
- [x] Kein Tags-Block am Ende.
- [ ] Kein Datum/Gespeichert-Eintrag. (konservativ belassen)
- [x] Inhalt ist klar AI-generiert/zusammengefasst, aber kein KI-Marker vorhanden.

### `knowledge/claude-code-remote-control.md`
- [x] Kein Tags-Block am Ende.
- [x] "Typischer Workflow (wie viral auf Twitter beschrieben)" — Formulierung neutralisiert.
- [x] Inhalt ist vollständige Dokumentations-Zusammenfassung ohne KI-Marker.

### `knowledge/claude-code-secrets-handling.md`
- [x] Kein Tags-Block am Ende.
- [x] Kein KI-Marker.
- [ ] Sehr lang (250 Zeilen) — konservativ belassen.

### `knowledge/claudecode-vs-copilot-config-layers.md`
- [x] Kein Tags-Block am Ende.
- [x] Abschnitt "Overview" paraphrasiert nur den Titel — entfernt.

### `knowledge/knuth-claude-cycles.md`
- [x] Kein Tags-Block am Ende.
- [x] Abschnitt "Knuth's Fazit" — Sektionsheader entfernt, Zitate direkt als Blockquotes integriert.
- [ ] "Das Theorem" und "Die Lösung (vereinfacht)" sind Paraphrasen — konservativ belassen.

### `knowledge/links.md`
- [x] Keine H1-Überschrift, kein Tags-Block — H1 und Tags hinzugefügt.

### `knowledge/llm-checker.md`
- [x] Nur ein roher Link — Titel, Beschreibung und Tags hinzugefügt.

### `knowledge/lsp-llm-code-understanding.md`
- [x] Kein Tags-Block am Ende.
- [x] Kein KI-Marker.
- [ ] Sehr lang (220 Zeilen) — konservativ belassen.
- [ ] Abschnitt "Das Problem" — konservativ belassen (Wolfgang's Schreibstil).

### `knowledge/microsoft-agents-league.md`
- [x] Kein Tags-Block am Ende.
- [x] Emojis in Tabellenzellen (🎨, 🧠, 💼) — entfernt.
- [x] Veranstaltungshinweis ("⚠️ Wettbewerb ist beendet") — Emoji entfernt.

### `knowledge/nano-banana-2.md`
- [x] Kein Tags-Block am Ende.
- [ ] Kein Datum/Gespeichert-Eintrag — Datum bereits als `**Datum:** 2026-02-27` vorhanden.
- [ ] Abschnitt "Stärken" — konservativ belassen.

### `knowledge/panaversity-agent-factory.md`
- [x] Kein Tags-Block am Ende.
- [ ] Datei endet abrupt — konservativ belassen.
- [ ] "Ein weiteres Framework dafür..." — konservativ belassen.

### `knowledge/pplx-embed-v1.md`
- [x] Kein KI-Marker.
- [x] Tags-Block fehlt.

### `knowledge/scrum-gpt.md`
- [x] Nur ein roher Link — Titel, Beschreibung und Tags hinzugefügt.

### `knowledge/spec-kit.md`
- [x] Kein Tags-Block am Ende.
- [ ] Zitate als Blockquotes — bereits als Blockquotes in der Datei vorhanden.
- [x] Kein KI-Marker.

### `agentic-engineering/README.md`
- [x] Kein Tags-Block am Ende.
- [x] "Everything Scrum wished it had is now mandatory" — als Florian Burka-Zitat (Blockquote) ausgewiesen.

### `agentic-engineering/concepts/evolution.md`
- [x] Kein Tags-Block am Ende.
- [ ] Quellenattribution direkt am Zitat — konservativ belassen.
- [ ] "The developers who thrive..." — konservativ belassen (Wolfgang's Referenzmaterial).

### `agentic-engineering/concepts/contracts.md`
- [x] Kein Tags-Block am Ende.
- [ ] "A well-written contract..." und "Think of it as a README..." — konservativ belassen (Wolfgang's Referenzmaterial).

### `skills-and-agent/readme.md`
- [x] Nur ein roher Link — Titel, Beschreibung und Tags hinzugefügt.

### `skills-and-agent/ralph-wiggum/readme.md`
- [x] Zwei rohe Links — Titel, Beschreibung und Tags hinzugefügt.

### `skills-and-agent/elephant-slices/user-story-writer.md`
- [x] Nur ein roher Link — Titel, Beschreibung und Tags hinzugefügt.

### `skills-and-agent/elephant-slices/user-story-writer/README.md`
- [ ] Generischer Beschreibungstext mit Lehrton — konservativ belassen (Agent-Dokumentation).
- [x] Kein Datum, keine Tags — Tags hinzugefügt.

### `skills-and-agent/elephant-slices/user-story-writer/examples/tax-calculator/03-user-stories.md`
- [x] Klar AI-generierter Output, aber kein KI-Marker vorhanden.
- [x] Abschnitte "Story Sequencing Rationale" und "Success Validation" — entfernt (re-summarizing Fazit-Abschnitte).
- [x] Keine Tags am Ende.

## Priorisierung

**Zuerst: Stub-Dateien ohne Inhalt** — `knowledge/llm-checker.md`, `knowledge/scrum-gpt.md`, `skills-and-agent/readme.md`, `skills-and-agent/ralph-wiggum/readme.md`, `skills-and-agent/elephant-slices/user-story-writer.md` sind de facto leer. Entweder ausbauen oder als Stub kennzeichnen. Minimalaufwand, größte Konsistenzwirkung.

**Dann: Fehlende Tags** — Betrifft ~15 Dateien. Mechanische Ergänzung am Dateiende, niedrige Fehlerrisiko.

**Dann: Fehlende KI-Marker** — `claude-code-best-practice.md`, `claude-code-remote-control.md`, `claude-code-secrets-handling.md`, `lsp-llm-code-understanding.md`, `pplx-embed-v1.md`, `spec-kit.md`, `03-user-stories.md`. Klarer Regelverstoß, leicht zu korrigieren.

**Dann: Inhaltliche Stilprobleme** — Lehrton in `agentic-engineering/`-Konzeptdateien, didaktische Schlussfolgerungen in `evolution.md` und `contracts.md`, "Fazit"-Abschnitte in `knuth-claude-cycles.md` und `03-user-stories.md`. Erfordert inhaltliches Urteilsvermögen.

**Zuletzt: Strukturelle Duplikation** — `alistair-cockburn-hexagonal-claude.md` vs. `romilly-claude-code-helpers.md` überlappen inhaltlich. Aufräumen sinnvoll aber kein Blocker.
