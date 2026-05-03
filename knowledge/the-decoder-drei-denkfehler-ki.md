---
URL: https://the-decoder.de/selbst-die-neuesten-ki-modelle-machen-drei-systematische-denkfehler-zeigt-neue-analyse/
Gespeichert: 2026-05-03
Autor: Matthias Bastian
Datum: 2026-05-02
---

# Selbst die neuesten KI-Modelle machen drei systematische Denkfehler

ARC Prize Foundation: 160 Testläufe mit GPT-5.5 und Opus 4.7 auf ARC-AGI-3. Scores: GPT-5.5 0,43 %, Opus 4.7 0,18 %. Die Fehler sind keine Capability-Lücken — sie sind strukturell.

---

**1. Lokale Beobachtung ohne globales Verständnis**

Modelle erkennen Einzeleffekte korrekt, synthetisieren sie aber nicht zu einem kohärenten Weltmodell. Opus 4.7 erkannte, dass ACTION3 einen Behälter dreht und ACTION5 Farbe ausschüttet — aber kombinierte beides nie zur nötigen Sequenz: drehen, dann ausschütten.

**2. Trainingsdaten erzeugen falsche Analogien**

Unbekannte Umgebungen werden reflexartig als bekannte Spiele klassifiziert — Tetris, Frogger, Sokoban, Breakout. GPT-5.5 interpretierte eine Umgebung mit Schlüsselkombinationen als Breakout und verschwendete Aktionen auf falsche Mechaniken.

**3. Gelöste Level erzeugen kein Verständnis**

Erfolg ohne Verifikation *warum* eine Lösung funktioniert führt zu falschen Theorien. Opus löste Level 1 mit einer falschen "Teleportations"-Hypothese. Level 1 gelang trotzdem — damit wurde die falsche Theorie bestätigt und auf Level 2 übertragen.

---

> "Scores zeigen was ein Modell erreicht hat. Replays zeigen, ob das Reasoning wahrscheinlich generalisiert."
> — ARC Prize Foundation

Gestützt durch: Apple Researcher, kognitionswissenschaftliche Analyse von 171.000 Reasoning-Traces, medizinische KI-Tests.

#ki #reasoning #arc-agi #denkfehler #kognition #type/note/analysis
