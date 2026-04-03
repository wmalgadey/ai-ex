---
URL: https://www.linkedin.com/pulse/10-harness-patterns-agents-run-days-instead-seconds-daniel-meyer-khj1e
Gespeichert: 2026-03-28
Autor: Daniel Meyer (CTO, Camunda)
---

# 10 Agent Harness Patterns


> "The hard part isn't the model anymore — it's the system around the model."

Der **Agent Harness** ist die Infrastruktur um das LLM herum — Orchestrierung, State, Fehlerbehandlung, Human-in-the-Loop. Meyer argumentiert mit etablierten Orchestrierungs-Engines (Camunda/Zeebe) als Referenz, aber die Patterns sind generisch.

> "The orchestration engine is the harness. The LLM is the horse."

---

## Die 10 Patterns

**1. Crash Resume** — Durable Execution
Jede Zustandsänderung ins Append-Only-Log. Bei Absturz: Log replay, Agent setzt bei Schritt 47 fort.

**2. Undo Chain** — Saga Pattern
Für jeden Schritt eine kompensierende Aktion definieren. Schlägt Schritt 3 fehl, rollt die Engine automatisch zurück.

**3. Patient Wait** — Event-Driven Sleep
Prozess "dehydriert" während Wartezeit — kein Memory, keine CPU, null Kosten. Wird bei Event geweckt.

**4. Autonomy Dial** — Business Rules außerhalb des Codes
Autonomie als Regler, nicht Schalter. Schwellenwerte in Decision Tables — änderbar ohne Code-Deployment.

> "Agent autonomy shouldn't be a binary. It should be a dial — and the rules for where that dial sits should live outside the agent's code."

**5. Fan-out Join** — Parallel Gateway mit Synchronisierung
Parallele Teilaufgaben, Engine trackt Completion, behandelt partielle Fehler, feuert Join genau einmal.

> "Surprisingly hard to build correctly from scratch."

**6. Mid-flight Upgrade** — Process Instance Migration
10.000 laufende Instanzen auf neue Agenten-Logik migrieren ohne State-Verlust. Beide Versionen laufen gleichzeitig.

**7. Escalation Clock** — Timer-basierte Eskalation
Timer direkt an Tasks — kein Cron-Job, kein externer Scheduler. Eskalationsregeln im Prozessdiagramm sichtbar.

**8. Scoped Delegation** — Variable Scoping zwischen Agenten
Jeder Agent bekommt genau den Kontext, den er braucht. Informationsgrenzen werden zur Design-Zeit definiert.

**9. Human Gate** — User Task als First-Class Primitive

> "This is not 'send a Slack message and hope.'"

Assignment-Logik, strukturierte Formulare, SLAs, Eskalation.

> "Building this from scratch means building a task management system. That's a product, not a feature."

**10. Audit Replay** — Immutable Process History
Regulierer fragt warum die KI eine Entscheidung getroffen hat → Prozessinstanz öffnen, jeden Schritt mit Variablen, Timestamps, Inputs, Outputs ansehen.

---

_Generiert anhand von LinkedIn-Artikel, 2026-03-28. Artikel ist Camunda-Advertorial, Patterns sind generisch anwendbar._

#agents #orchestration #patterns #durable-execution #agentic-engineering #production
