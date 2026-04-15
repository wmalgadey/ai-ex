---
URL: https://wuesteon.github.io/blog/posts/de/karpathy-claude-md.html
Gespeichert: 2026-04-15
---

# Karpathy CLAUDE.md — 25.000 Sterne

_Nils Weiser · wuesteon.github.io · 14. April 2026_

Ein GitHub-Repo, das nichts enthält außer einer einzigen CLAUDE.md-Datei, steht bei über 25.000 Sternen. Kein Framework, keine CLI, kein Python-Paket. Nur Text.

GitHub: [forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills)

---

## Karpathys Diagnose (aus dem Repo)

> "Die Modelle treffen falsche Annahmen für dich und laufen damit einfach los, ohne nachzufragen. Sie managen ihre eigene Unsicherheit nicht, bitten nicht um Klärung, zeigen keine Inkonsistenzen auf, präsentieren keine Tradeoffs, widersprechen nicht, wenn sie sollten."

> "Sie neigen stark dazu, Code und APIs zu überkomplizieren, Abstraktionen aufzublähen, toten Code nicht aufzuräumen... und bauen auf 1000 Zeilen, was in 100 gegangen wäre."

> "Sie ändern oder entfernen manchmal noch Kommentare und Code, den sie nicht ausreichend verstanden haben, als Seiteneffekt — selbst wenn das mit der eigentlichen Aufgabe nichts zu tun hat."

---

## Die vier Prinzipien

**1. Think Before Coding**  
Annahmen explizit machen. Bei Mehrdeutigkeit mehrere Interpretationen nennen statt still eine zu wählen. Bei einfacherem Weg widersprechen. Bei Unklarheit stoppen und fragen.

**2. Simplicity First**  
Nur der Code, der die Aufgabe löst. Keine Features auf Verdacht. Keine präventiven Abstraktionen. Kein Error-Handling für unmögliche Fälle. Wenn 50 Zeilen auch gehen, 200 umschreiben.

**3. Surgical Changes**  
Nur anfassen, was angefasst werden muss. Bestehenden Stil übernehmen. Kein "Aufräumen" am Rand der Aufgabe. Jede geänderte Zeile muss sich auf den Auftrag zurückführen lassen.

**4. Goal-Driven Execution**  
Erfolgskriterien vor Code. "Fix den Bug" → "Schreibe einen Test, der den Bug reproduziert, und bring ihn zum Grün." Starke Kriterien erlauben autonome Iteration.

---

## CLAUDE.md vs. Skills

| | CLAUDE.md | Skills |
|---|---|---|
| Wann aktiv | Immer im Kontext | On-Demand geladen |
| Zweck | Generelles Verhalten | Konkrete Workflows |
| Scope | Projektweit | Aufgabenspezifisch |
| Ideal für | Stil, Disziplin, Do's und Don'ts | Tools, Scripte, spezifische Domänen |

> "Eine schlanke CLAUDE.md mit Verhaltensregeln plus ein Satz Skills für die tatsächlichen Werkzeuge ist das Setup, das am zuverlässigsten funktioniert."

---

## Warum 25.000 Sterne

> "'KI nutzen, um Code zu schreiben' war die Phase der letzten zwei Jahre. 'Das Verhalten der KI so formen, dass der Code tatsächlich gut wird' ist die Phase, in die wir gerade eintreten."

> "Die besten Werkzeuge im Claude-Code-Ökosystem sind aktuell keine Software. Es sind gut durchdachte Anweisungen."

---

## Technik: Wie die Seite gebaut wurde

GitHub Pages + **Tailwind CSS via CDN** (`cdn.tailwindcss.com`) + handgeschriebenes HTML. Kein erkennbarer Static Site Generator (kein Hugo-Meta, kein Jekyll-Kommentar im Source). Vermutlich manuell oder mit eigenem Minimal-Build-Skript. URL-Struktur `/blog/posts/de/` deutet auf eigene Ordnerkonvention hin.

Prinzip-Cards: `background: linear-gradient(135deg, rgba(6,182,212,0.05), rgba(34,197,94,0.05))` — subtiler Teal/Green-Gradient + Cyan-Border.

---

## Verwandt

- [Claude Prompting Best Practices](claude-prompting-best-practices.md) — Anthropics offizielle Guidance zu Claude 4.x
- [Karpathy LLM Wiki](../knowledge/karpathy-llm-wiki.md) — Karpathys Ingest/Query/Lint-Pattern für Semantic Memory

#claude-code #claude-md #karpathy #prompting #skills #best-practices
