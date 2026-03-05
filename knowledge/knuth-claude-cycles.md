# Don Knuth: "Claude's Cycles" — Ein Wendepunkt?

**Datum:** 28. Februar 2026 (revised 4. März 2026)  
**Autor:** Don Knuth, Stanford  
**Paper:** https://cs.stanford.edu/~knuth/papers/claude-cycles.pdf  
**LinkedIn-Post:** https://www.linkedin.com/posts/barbaralampl_say-what-don-knuth-will-seine-sicht-auf-share-7435216114999214081-Qw02

---

## Worum geht's?

Don Knuth (88, Autor von *The Art of Computer Programming*, eine der einflussreichsten Figuren der Informatik) hat bisher GenAI eher skeptisch beurteilt. Am 28. Februar 2026 veröffentlichte er eine kurze Note mit dem Titel *"Claude's Cycles"* — und der Ton ist ein komplett anderer.

**Sein Einstieg:** "Shock! Shock! I learned yesterday that an open problem I'd been working on for several weeks had just been solved by Claude Opus 4.6."

---

## Das Problem

Knuth arbeitete an einem kombinatorischen Problem für ein zukünftiges Volume von *The Art of Computer Programming*:

Gegeben sei ein gerichteter Graph mit m³ Knoten `ijk` (mit 0 ≤ i, j, k < m), und drei Kanten von jedem Knoten — zu `i+jk`, `ij+k` und `ijk+` (wobei `i+` = (i+1) mod m bedeutet). Gesucht: eine allgemeine Zerlegung der Kanten in drei gerichtete m³-Zyklen, für alle m > 2.

Knuth hatte es für m = 3 gelöst. Sein Freund Filip Stappers fand empirisch Lösungen für 4 ≤ m ≤ 16. Dann fragte Stappers Claude Opus 4.6 — mit dem exakten Wortlaut des Problems plus strukturiertem Coaching (z. B. nach *jedem* Explorationsschritt erst `plan.md` updaten).

---

## Wie Claude das gelöst hat

Claude machte 31 Explorationsschritte (exploreXX.py), dokumentiert in einer plan.md. Der Weg:

1. **Reformulierung** als Sigma-Funktion: Z³ₘ → S₃ (Permutation der drei Richtungen pro Knoten)
2. **Lineare/quadratische Ansätze** → Sackgasse
3. **DFS Brute-Force** für m=3 → zu langsam
4. **2D Serpentine** — hier erkannte Claude das Problem als Cayley-Digraph (Gruppentheorie!)
5. **Simulated Annealing** für mehrere m
6. **Fazit nach Exploration 25:** "SA can find solutions but cannot give a general construction. Need pure math."
7. **Exploration 31:** Konkreter Konstruktionsalgorithmus als Python-Programm — funktioniert für alle ungeraden m = 3, 5, 7, 9, 11

**Stappers testete das Python-Programm für alle ungeraden m zwischen 3 und 101 — perfekte Zerlegungen in jedem Fall.**

---

## Die Lösung (vereinfacht)

Die Richtungswahl hängt ab von s = (i+j+k) mod m:

- **s = 0:** bump i wenn j = m-1, sonst bump k
- **0 < s < m-1:** bump k wenn i = m-1, sonst bump j
- **s = m-1:** bump j wenn i > 0, sonst bump k

("Bump" = mod m inkrementieren)

Das Ganze als C-Programm (von Knuth vereinfacht) — weniger als 20 Zeilen.

---

## Das Theorem

Knuth formalisiert Claudes Ansatz als *"Claude-like decomposition"*: Permutationen hängen nur davon ab, ob i, j, s gleich 0 oder m-1 oder etwas dazwischen sind.

**Theorem:** Eine Claude-like Zerlegung ist für alle ungeraden m > 1 gültig ↔ jede der drei Sequenzen für m=3 ist "generalizable" (d.h. sie lässt sich systematisch auf alle ungeraden m ausweiten).

**Offenes Problem:** Für gerade m ist die Frage noch offen. m=2 ist unmöglich (seit langem bewiesen). Claude fand Lösungen für m=4, 6, 8 — konnte aber keine allgemeine Konstruktion liefern.

---

## Knuth's Fazit

> "All in all, however, this was definitely an impressive success story."

Er schreibt auch: "It seems that I'll have to revise my opinions about 'generative AI' one of these days."

Und am Ende: "Hats off to Claude!"

---

## Warum das relevant ist

- **Knuth ist nicht irgendwer.** Er hat Jahrzehnte lang skeptisch auf AI-Hype reagiert. Sein Meinungsumschwung hat Gewicht.
- **Das ist echte Mathematik**, kein Coding-Task. Claude hat selbstständig strukturierte Exploration betrieben, Sackgassen erkannt, Hypothesen geformt und schließlich eine beweisbare Konstruktion gefunden.
- **Kombination Mensch + AI:** Stappers coached Claude (strukturiertes Dokumentieren), Knuth formalisierte das Ergebnis. Das ist kollaborative Mathematik.
- **Modell:** Claude Opus 4.6 (Hybrid Reasoning, released ~Anfang Februar 2026)
- **Shift in der Debatte:** Barbara Lampl bringt es auf den Punkt — die Frage ist nicht mehr "Was kann AI?", sondern "Wie reliable ist AI als Werkzeug für echte Forschung?"

---

## Links

- Paper (Stanford): https://cs.stanford.edu/~knuth/papers/claude-cycles.pdf
- Don Knuth (Wikipedia): https://de.wikipedia.org/wiki/Donald_Knuth
- *The Art of Computer Programming*: https://www-cs-faculty.stanford.edu/~knuth/taocp.html
