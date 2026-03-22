# Article Review Plan
_Generated: 2026-03-22_

## Zusammenfassung
22 files OK, 18 files need changes

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
- [ ] Kein Tags-Block am Ende — fehlt komplett.
- [ ] Workflow-Phasen sind paraphrasiert, nicht aus dem Original zitiert; direktere Auszüge wären laut Style Guide vorzuziehen.

### `knowledge/alistair-cockburn-hexagonal-claude.md`
- [ ] Tags-Abschnitt steht in der Mitte des Dokuments, nicht am Ende — muss ans Ende verschoben werden.
- [ ] Abschnitt "Verwandte Ressourcen" enthält duplizierten Inhalt zu `romilly-claude-code-helpers.md`; wäre besser als reiner Link statt ausführlicher Inhaltswiedergabe.
- [ ] "Was ist das?" + "Interessant für:"-Zeile formuliert explizit, warum es interessant ist — verstößt gegen Chronisten-Perspektive (kein "was man daraus lernen soll").
- [ ] "Notizen"-Abschnitt ganz unten passt nicht zur Struktur; besser in Frontmatter oder weg.

### `knowledge/anthropic-courses.md`
- [ ] Keine Tags am Ende.
- [ ] Kein Datum/Gespeichert-Eintrag.
- [ ] Keine Quelle als Frontmatter-Block, nur URL-Zeile ohne Label — inkonsistent mit Konvention.

### `knowledge/bmad-method.md`
- [ ] Slogans direkt aus dem Repo zitiert ("Breakthrough Method..."), aber nicht als Blockquote ausgewiesen — optisch unklar, ob Paraphrase oder Zitat. Sollte als `>` blockquote formatiert werden.
- [ ] "100% free & open source. Keine Paywalls." — wertende Aussage ohne Quellenangabe; eher Paraphrase als Chronik-Eintrag.
- [ ] Kein Tags-Block am Ende.

### `knowledge/claude-code-best-practice.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Kein Datum/Gespeichert-Eintrag.
- [ ] Inhalt ist klar AI-generiert/zusammengefasst (Feature Map, Best Practices in Listenform aus einem Repo extrahiert), aber kein KI-Marker vorhanden.

### `knowledge/claude-code-remote-control.md`
- [ ] Kein Tags-Block am Ende.
- [ ] "Typischer Workflow (wie viral auf Twitter beschrieben)" — anekdotisch, ohne Quellenlink. Entweder Quelle ergänzen oder Formulierung neutralisieren.
- [ ] Inhalt ist vollständige Dokumentations-Zusammenfassung ohne KI-Marker, obwohl deutlich aus Docs rekonstruiert.

### `knowledge/claude-code-secrets-handling.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Kein KI-Marker — Inhalt ist offensichtlich aus Dokumentation und Best-Practice-Quellen zusammengefasst/generiert.
- [ ] Sehr lang (250 Zeilen) für ein knowledge/-Artikel; könnte auf Kernaussagen reduziert werden, Details ggf. per Link auf Docs.

### `knowledge/claudecode-vs-copilot-config-layers.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Abschnitt "Overview" paraphrasiert nur den Titel — überflüssiger Absatz, eliminieren.

### `knowledge/knuth-claude-cycles.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Abschnitt "Knuth's Fazit" am Ende fasst das Vorherige mit Zitaten zusammen — ein "Fazit"-Abschnitt ist laut Style Guide unerwünscht. Die Zitate können direkt in den Fließtext integriert werden.
- [ ] "Das Theorem" und "Die Lösung (vereinfacht)" sind Paraphrasen des Papers, keine direkten Zitate daraus — Style Guide fordert direkte Auszüge wo möglich.

### `knowledge/links.md`
- [ ] Keine H1-Überschrift, kein Datum, kein Tags-Block — minimale Stub-Datei, die kaum mehr als ein Lesezeichen ist. Entweder mit Grundstruktur versehen oder Inhalt in `knowledge/links.md` konsolidieren.

### `knowledge/llm-checker.md`
- [ ] Nur ein roher Link ohne jeglichen Kontext, Titel, Beschreibung oder Tags. Entweder als vollständiger Eintrag ausbauen oder löschen.

### `knowledge/lsp-llm-code-understanding.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Kein KI-Marker — Dokument ist erkennbar eine ausführliche Zusammenstellung/Recherche, nicht persönliche Beobachtung.
- [ ] Sehr lang (220 Zeilen); mehrere Unterabschnitte (Keel, GitLab KG) könnten eigene Dateien sein oder als reine Links verbleiben.
- [ ] Abschnitt "Das Problem" erklärt didaktisch was LLMs nicht können — Lehrton statt Chronisten-Perspektive.

### `knowledge/microsoft-agents-league.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Emojis in Tabellenzellen (🎨, 🧠, 💼) — nicht im Style Guide vorgesehen; entfernen.
- [ ] Veranstaltungshinweis ("⚠️ Wettbewerb ist beendet") als Emoji-Warnung — besser als einfache Notiz ohne Emoji.

### `knowledge/nano-banana-2.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Kein Datum/Gespeichert-Eintrag im Frontmatter-Format (Datum nur im H1-Bereich).
- [ ] Abschnitt "Stärken" listet Marketing-Claims aus der Quelle ohne Blockquote-Kennzeichnung.

### `knowledge/panaversity-agent-factory.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Datei endet abrupt — kein abschließender Kontext, kein Datum.
- [ ] "Ein weiteres Framework dafür..." — wertende Aussage (implizit skeptisch), was in Ordnung wäre wenn klar als persönliche Einschätzung erkennbar; hier aber im Fließtext versteckt.

### `knowledge/pplx-embed-v1.md`
- [ ] Kein KI-Marker — Inhalt ist klar aus Artikel/Release-Announcement zusammengefasst.
- [ ] Datei endet ohne abschließende Zeile/Tags — Tags-Block fehlt.

### `knowledge/scrum-gpt.md`
- [ ] Nur ein roher Link ohne Titel, Beschreibung, Datum, Tags. Gleiche Problematik wie `llm-checker.md`.

### `knowledge/spec-kit.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Zitate aus dem Repo (`"Build high-quality software faster."`, `"An open source toolkit..."`) sollten als Blockquotes formatiert sein, stehen aber im Fließtext.
- [ ] Kein KI-Marker, obwohl Inhalt klar aus Dokumentation zusammengefasst wurde.

### `agentic-engineering/README.md`
- [ ] Kein Tags-Block am Ende (für ein README weniger kritisch, aber der Style Guide gilt für alle .md-Dateien im Repo).
- [ ] "Everything Scrum wished it had is now mandatory" — assertive Aussage ohne Quellenangabe; sollte als Florian Burka-Zitat ausgewiesen sein.

### `agentic-engineering/concepts/evolution.md`
- [ ] Kein Tags-Block am Ende.
- [ ] Abschnitt "Key Insight" enthält ein deutsches Zitat (`"Das Muster ist immer gleich..."`), das als Blockquote formatiert ist — gut. Aber Quellenattribution ist nur im H1 "Source:"-Link, nicht direkt am Zitat.
- [ ] "The developers who thrive are those who build the verification harness *first*..." — didaktische Schlussfolgerung, nicht aus der Quelle zitiert; Chronisten-Perspektive verletzt.

### `agentic-engineering/concepts/contracts.md`
- [ ] Kein Tags-Block am Ende.
- [ ] "A well-written contract is the single highest-leverage investment you can make." — nicht aus einer Quelle zitiert, wirkt wie redaktionelle Meinung; sollte entweder als persönliche Einschätzung markiert oder entfernt werden.
- [ ] "Think of it as a README written for an agent..." — erklärende Analogie im Lehrton, nicht Chronisten-Perspektive.

### `skills-and-agent/readme.md`
- [ ] Nur ein roher Link ohne Kontext. Gleiche Problematik wie `llm-checker.md` und `scrum-gpt.md`.

### `skills-and-agent/ralph-wiggum/readme.md`
- [ ] Zwei rohe Links ohne Titel, Kontext, Datum, Tags.

### `skills-and-agent/elephant-slices/user-story-writer.md`
- [ ] Nur ein roher Link — kein Inhalt, kein Datum, keine Tags.

### `skills-and-agent/elephant-slices/user-story-writer/README.md`
- [ ] Generischer Beschreibungstext mit Lehrton ("Use this agent when:", "This agent transforms...") — kein Chronisten-Blick, sondern Dokumentations-Marketing-Stil.
- [ ] Kein Datum, keine Tags.

### `skills-and-agent/elephant-slices/user-story-writer/examples/tax-calculator/03-user-stories.md`
- [ ] Klar AI-generierter Output (User Stories von einem Agent), aber kein KI-Marker vorhanden.
- [ ] Abschnitte "Story Sequencing Rationale" und "Success Validation" am Ende sind klassische "Fazit"-Abschnitte die das Vorherige zusammenfassen — laut Style Guide unerwünscht.
- [ ] Keine Tags am Ende.

## Priorisierung

**Zuerst: Stub-Dateien ohne Inhalt** — `knowledge/llm-checker.md`, `knowledge/scrum-gpt.md`, `skills-and-agent/readme.md`, `skills-and-agent/ralph-wiggum/readme.md`, `skills-and-agent/elephant-slices/user-story-writer.md` sind de facto leer. Entweder ausbauen oder als Stub kennzeichnen. Minimalaufwand, größte Konsistenzwirkung.

**Dann: Fehlende Tags** — Betrifft ~15 Dateien. Mechanische Ergänzung am Dateiende, niedrige Fehlerrisiko.

**Dann: Fehlende KI-Marker** — `claude-code-best-practice.md`, `claude-code-remote-control.md`, `claude-code-secrets-handling.md`, `lsp-llm-code-understanding.md`, `pplx-embed-v1.md`, `spec-kit.md`, `03-user-stories.md`. Klarer Regelverstoß, leicht zu korrigieren.

**Dann: Inhaltliche Stilprobleme** — Lehrton in `agentic-engineering/`-Konzeptdateien, didaktische Schlussfolgerungen in `evolution.md` und `contracts.md`, "Fazit"-Abschnitte in `knuth-claude-cycles.md` und `03-user-stories.md`. Erfordert inhaltliches Urteilsvermögen.

**Zuletzt: Strukturelle Duplikation** — `alistair-cockburn-hexagonal-claude.md` vs. `romilly-claude-code-helpers.md` überlappen inhaltlich. Aufräumen sinnvoll aber kein Blocker.
