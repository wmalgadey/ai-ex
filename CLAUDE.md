# ai-ex — Schreibstil & Konventionen

Dieses Repo dokumentiert KI-Werkzeuge, Konzepte und persönliche Erfahrungen. Kein Tutorial-Blog, kein Marketing, keine Zusammenfassungen für Leute die nicht selbst lesen wollen.

## Schreibstil

**Chronisten-Perspektive.** Was wurde gefunden, wann, warum interessant. Nicht: was es bedeutet, was man daraus lernen soll.

**Kurz.** Artikel sollen knapp sein. Kernpunkte, keine Ausschweifungen. Wenn ein Satz reicht, kein Absatz.

**Kein KI-Schreibstil.** Keine Adverbien zur Dramatisierung ("was folgte war..."), keine Superlative, keine rhetorischen Fragen, keine "Fazit"-Abschnitte die das Vorherige nochmal zusammenfassen. Sachlich.

**Zitate und Auszüge statt Paraphrasen.** Kernaussagen aus der Quelle direkt übernehmen — als Blockquote oder Code-Block. Nicht umschreiben.

**Grafiken und Architektur-Diagramme** aus der Quelle einbinden wenn vorhanden (als Link oder eingebettetes Bild).

## Bei KI-generierten Artikeln

Kennzeichnen mit:
```
_Rekonstruiert aus [Quelle], [Datum]._
```
oder
```
_Generiert anhand von [Quelle/Konversation], [Datum]._
```

## Struktur

```
knowledge/            — Werkzeuge, Konzepte, Recherche (externe Quellen)
journal/              — Persönliche Erfahrungen, Entscheidungen, Journey
agentic-engineering/  — Konzepte und Praxis rund um agentic software development
skills-and-agent/     — Konkrete Skills und Agent-Implementierungen
```

## YAML-Frontmatter (optional, aber hilfreich)

```
---
URL: [Quelle]
Gespeichert: YYYY-MM-DD
---
```

## Tags

Am Ende jedes Artikels, eine Zeile, Hashtags.

## Struktur & Navigation

Jeder Ordner hat eine `README.md` (von GitHub automatisch angezeigt) und thematische MOC-Dateien.

**README.md je Ordner:** Kurze Beschreibung des Bereichs + Links zu den thematischen MOCs.

**Thematische MOCs:** Liste von Artikeln zu einem Themenfeld — `[Titel](dateiname.md)` + eine Zeile Beschreibung.

**Beim Erstellen neuer Artikel:**
1. Artikel in die passende thematische MOC eintragen — Titel als Link + eine Zeile Beschreibung, sachlich, kein KI-Stil.
2. In der **Hauptdatei `README.md`** in der Tabelle das Datum der geänderten MOC-Zeile auf das heutige Datum setzen — das Datum gibt an, wann die MOC zuletzt inhaltlich geändert wurde, nicht wann die README-Tabelle bearbeitet wurde.
3. Wenn ein neuer Artikel einem neuen Themenbereich entspricht, neue MOC-Datei anlegen und in `README.md` einführen.

**Journal-Einträge (`journal/`):**
- Jeden neuen Journal-Eintrag immer auch in `journal/README.md` unter "Artikel" eintragen — Titel als Link + eine Zeile Beschreibung.
- Zusätzlich das Datum der `journal/README.md`-Zeile in der Haupt-`README.md`-Tabelle aktualisieren.
