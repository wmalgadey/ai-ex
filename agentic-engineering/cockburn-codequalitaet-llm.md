---
URL: https://www.linkedin.com/posts/alistaircockburn_the-question-on-my-mind-is-who-cares-share-7451031987361894400-eOvs
Gespeichert: 2026-04-18
---

# Cockburn: Spielt Code-Qualität noch eine Rolle?

_Rekonstruiert aus LinkedIn-Post und verlinkter ChatGPT-Konversation, 2026-04-18._

## Die Provokation

Alistair Cockburn (Erfinder von Hexagonal Architecture, Crystal, Heart of Agile) stellt die Frage öffentlich:

> "the question on my mind is: who cares about code quality if the LLM is just going to regenerate it each time? Does it matter how good the coupling and cohesion are? The class names and their separation?"

> "UPDATE: after seeing some of the comments, I note that they are still missing any argument for code quality as we have been defining it for the last 40 years. So I'm doubling down and claiming (only for the sake of having a proper, informative debate) that code quality doesn't matter."

> "p.s. if you only talk about the tests, that's not relevant to the question and I'll ignore your answer. Think of the spectrum from big ball of mud through small balls of mud to fabulous DDD — where, when, why does it matter?"

## Das Experiment (Cockburns eigenes Folge-Posting)

Cockburn verlinkt in den Kommentaren eine ChatGPT-Konversation: https://chatgpt.com/share/69e2f3cb-b090-83ea-a014-4f6ed1dc776a

Aufgabe: ein kleines Java-Programm mit Hexagonal Architecture (kürzestes Gedicht eines Poeten aus DB). Zwei Varianten:

- **Program #1 — Clean Code / DDD**: vollständige Domain-Modellierung, benannte Klassen, DDD-Konventionen, "be proud of this"
- **Program #2 — Tight Code**: hexagonale Architektur bleibt, aber so wenige Klassen und Funktionen wie möglich, terse

Drei Fragen: Token-Kosten bei der Generierung, Lesbarkeit als Input, Modifizierbarkeit bei Anforderungsänderungen.

### Befunde

**Token-Kosten:** Program #1 ~2.000 Token, Program #2 ~800 Token — Faktor ~2,5x günstiger für kompakten Code.

**Lesbarkeit als Input:** Program #2 gewinnt bei einfachen, stabilen Domänen. Program #1 gewinnt wenn viele Zuständigkeiten separat nachvollzogen werden müssen.

**Modifizierbarkeit:** Hier liegt das Kernproblem. ChatGPTs Antwort:

> "Locating lines is cheap; understanding coupling is expensive."

> "A compact single function is easy when it contains one real idea. It becomes harder when it contains five ideas braided together."

> "The right variable is not only size. It is entanglement."

Konkret:
- **Re-reading cost** (wie viele Token kostet es, den alten Code wieder zu konsumieren): Program #2 gewinnt klar
- **Editing-risk cost** (wie schwer ist es, korrekt zu ändern ohne Nebeneffekte): Program #1 gewinnt oft — mehr Struktur = offensichtlicheres Zuhause für neue Regel

> "Program 2 minimizes re-input cost. Program 1 often minimizes conceptual risk during change. Those are not the same thing."

## Das Paradox

Cockburn hat Hexagonal Architecture erfunden — als Antwort auf schlechtes Coupling, versteckte Abhängigkeiten, schwer testbaren Code. Jetzt fragt er, ob genau das für LLMs noch relevant ist.

Die ChatGPT-Konversation gibt eine differenzierte Antwort: **Kompakter Code ist tokenökonomisch effizienter. Strukturierter Code zahlt sich aus, wenn Anforderungsänderungen verschiedene Zuständigkeiten unabhängig voneinander treffen.**

Das ist kein Widerspruch zu 40 Jahren Software-Handwerk — aber es verschiebt den Begründungsrahmen. Die Frage ist nicht mehr "was ist für Menschen lesbar" sondern "was kostet es, dem Modell zu erklären was geändert werden soll". Und diese Metrik begünstigt anders als manche erwartet hätten nicht immer DDD.

## Verwandte Artikel

- [Alistair Cockburn – Hexagonal Architecture mit Claude](alistair-cockburn-hexagonal-claude.md)
- [Scrum at Machine Speed – Waterfall Bias in LLMs](../scrum-at-machine-speed/chapter-04-waterfall-developers.md)

#code-quality #llm #hexagonal-architecture #ddd #token-economics #alistair-cockburn
