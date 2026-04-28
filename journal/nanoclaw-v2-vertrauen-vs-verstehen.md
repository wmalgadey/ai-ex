---
Gespeichert: 2026-04-29
---

# Welchem KI-Agenten-Framework vertraue ich — und warum *(begrenzte Auswahl)*

*Stil: Persönlich, erste Person, direkte Beobachtung — keine Superlative, kein explizites Fazit.*

Mein letzter Post zu OpenClaw wurde kontrovers aufgenommen. Ich verstehe das. Der Vergleich war unvollständig. Hier eine ehrlichere Version, nach dem Upgrade auf NanoClaw v2.

---

**Wie ich eine solche Entscheidung treffe:**

1. Lies die Codebase — nicht alles, aber genug um zu verstehen wie Nachrichten fließen und wo Entscheidungen fallen.
2. Zähle die beweglichen Teile: Quelldateien, Abhängigkeiten, Konfigurationsdateien. Nicht als Qualitätsurteil, sondern als Aufwandsschätzung.
3. Entscheide bewusst: Willst du das System *verstehen* oder ihm *vertrauen*? Beides ist eine legitime Antwort, aber sie führen zu unterschiedlichen Werkzeugen.
4. Baue eigene Erweiterungen. Wie einfach ist das? Wie stabil bleiben sie über Updates?
5. Beobachte Verhaltensänderungen nach Updates — waren sie erwartbar oder überraschend?
6. Prüfe das Release-Management: gibt es ein Changelog, Versioning, ein "stable"?
7. Entscheide anhand des Ergebnisses — nicht als Empfehlung für andere.

---

**Was bei NanoClaw v2 neu ist:**

Setup als deterministisches Script — kein Token-Verbrauch, kein LLM als Executor. Ein Container-Image je Agent, hash-basiert, mit persistenten Paketen via `install_packages`. Tailscale-Integration funktioniert. Supply Chain Security über pnpm mit `minimumReleaseAge: 4320` (3 Tage) für alle Abhängigkeiten.

Was ich in v1 selbst gebaut hatte — SSH-Keys, Plugin-System, manuelle Tailscale-Integration — ist in v2 Teil des Systems.

> "I wouldn't have been able to sleep if I had given complex software I didn't understand full access to my life."

Das ist der Kern. Nicht Features, nicht Performance.

**Was NanoClaw nicht löst:** Kein Release-Management. Kein gepflegtes Changelog. Man ist immer early adopter, immer Tester. OpenClaw hat das — zumindest kommuniziert es Updates.

---

**Zeitaufwand & Aufwand:** Schritte 1–2 dauern je nach Codebase-Größe 1 Stunde bis 2 Wochen; Schritte 3–7 sind einmalig, aber keine einmalige Entscheidung.

**Tools & Ressourcen:** • NanoClaw v2 (`bash nanoclaw.sh`), `install_packages`, `container.json`, `src/container-runner.ts`

**Häufige Fallstricke:** • Codebase-Größe mit Qualität gleichsetzen • Vertrauen durch Gewohnheit verwechseln • Release-Stabilität höher gewichten als Verständlichkeit — oder umgekehrt

**Beispiel:** In NanoClaw v2 bekommt jeder Agent ein eigenes Container-Image mit einem hash-basierten Slug. Das klingt nach Komplexität, ist aber das Gegenteil: wer wie ich ein eigenes Containerfile führt, merkt dass v2 genau das zum Standard macht — nachvollziehbar, reproduzierbar, ohne implizite Abhängigkeit auf "latest".

#nanoclaw #openclaw #agentic-ai #self-hosting #container
