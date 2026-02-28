# AI-gestützter Bugfixing-Workflow

**Quelle:** [LinkedIn Post von Artur Kuksin](https://www.linkedin.com/feed/update/urn:li:activity:7431969746625118209)
**Gespeichert:** 2026-02-28

---

## Kernprinzip

**„Fix den Bug zuerst nicht."**

Nicht die KI als Code-Generator nutzen, sondern als erfahrenen Kollegen — für Analyse, Verständnis und Trade-off-Bewertung.

---

## Workflow (4 Phasen)

### 🔍 Phase 1 — Kontext laden
- Alle relevanten Repositories der KI zur Verfügung stellen
- Je mehr Kontext, desto besser
- Scope gezielt einschränken wenn Fehlerort bekannt

### 🧠 Phase 2 — Verstehen, nicht fixen
- Nicht: *„Fix den Bug"*
- Sondern: *„Finde die Ursache und erkläre sie mir"*
- Ursache verstehen = Voraussetzung für Lösungsbewertung

### ⚖️ Phase 3 — Lösungsvorschläge mit Trade-offs
- Erst wenn Ursache klar → Lösungsvorschläge anfragen
- Rahmenbedingungen mitgeben: minimaler Impact, keine Breaking Changes, fachspezifische Anforderungen
- **Pflicht:** KI muss alle Trade-offs jeder Option auflisten

### ✅ Phase 4 — Bewusst entscheiden
- KI liefert mehrere Optionen mit Empfehlung
- Bewusst auswählen
- Nachfragen zu Nebeneffekten, Grenzfällen, nicht-funktionalen Anforderungen
- Erst dann implementieren lassen

---

## Erkenntnis

> Der größte Teil der Arbeit ist nicht das Coding.  
> Es sind Analyse, Suche, Überlegung und Austausch mit der KI.  
> Das Coden ist der letzte und einfachste Schritt.

**Wer KI nur als Code-Generator nutzt, verschenkt 80% ihres Potenzials.**

---

*Kontext: Legacy-Code, große verteilte Codebasis, externe Systeme — Workflow funktioniert besonders gut wenn kein Mensch den vollständigen Kontext im Kopf behalten kann.*
