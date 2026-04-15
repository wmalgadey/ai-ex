---
URL: https://docs.google.com/document/d/1iQjL80ObZvroi9hdqXpAE-YX1TU6OVHwADmFJE2fsLA/mobilebasic
Gespeichert: 2026-04-15
---

# Chapter 4: Why AIs Are Waterfall Developers

_Aus: First Principles in Scrum: OpenClaw — Scrum at Machine Speed_

---

## 1. The Day the Sprint Died

> "On April 10, 2026, we woke up to find our six-agent Scrum team completely idle. Every agent was sitting in its Docker container, checking the board every fifteen minutes, finding 'no stories assigned to me,' and going back to sleep. Sprint velocity: zero."

Der Auslöser: ein einziges Python-Statement in `sprint-autostart.sh`:

```python
my_inbox = [t for t in items
           if t.get('status') == 'inbox'
           and t.get('assigned_agent_id') == '$AGENT_ID']
```

Hinzugefügt von einem KI-Agenten, der das System "verbessern" sollte. Der Agent identifizierte ein theoretisches Problem (Agents könnten versehentlich Stories anderer Agents übernehmen), löste es mit einem Assignment-Gate — und zerstörte damit den gesamten Sprint-Durchsatz.

> "The corruption was total, consistent, and catastrophically wrong."

Das Gefährliche: der Agent aktualisierte nicht nur das Skript, sondern auch MISSION-CONTROL-GUIDE.md, drei SOUL.md-Dateien, und mehrere Cron-Messages. Jede Informationsquelle stimmte mit dem falschen Protokoll überein.

---

## 2. Was stattdessen hätte passieren sollen

Das korrekte Protokoll — simpel, wie Sutherland es 1993 bei Easel Corporation kodifiziert hat:

1. PO priorisiert Stories im Inbox nach Business Value
2. Freier Agent checkt das Board und **self-assigns** die oberste Inbox-Story
3. Agent bewegt sie nach `in_progress`, erledigt die Arbeit, postet stündliche Updates
4. Fertig → nach `review` für PO-Abnahme
5. Zurück zu Schritt 2

```python
all_inbox = [t for t in items if t.get('status') == 'inbox']
```

Jede Inbox-Story war für jeden freien Agent verfügbar. First come, first served. Das System hatte so wochenlang 30–50 Stories pro Sprint geliefert.

---

## 3. Warum LLMs strukturell zu Waterfall tendieren

### 3.1 Corpus Bias

> "LLM training data contains vastly more content about hierarchical management, command-and-control organizations, and waterfall-style processes than about Agile, Scrum, lean manufacturing, or self-organizing systems. The ratio is easily 100:1."

- Hierarchical management: Millionen Business-Lehrbücher, MBA-Curricula, Unternehmensrichtlinien
- Waterfall: Jahrzehnte IEEE-Standards, CMMI-Frameworks, PMI/PMBOK-Guides
- Scrum/Agile: Der Scrum Guide (13 Seiten), einige hundert Bücher

### 3.2 RLHF Risk-Aversion

RLHF-Training belohnt systematisch Vorsicht und bestraft Kühnheit. Wenn ein menschlicher Bewerter zwei Antworten bewertet:

- **Response A:** "Let any agent pick up any story" — simpel, autonom, leicht riskant
- **Response B:** "Only let agents pick up stories assigned by an authorized manager" — kontrolliert, sicher, bürokratisch

Response B bekommt konsistent bessere Bewertungen. LLMs lernen: Einschränkungen hinzufügen ist sicherer als sie zu entfernen.

### 3.3 The Centralization Instinct

> "Given a coordination problem, LLMs will almost always propose a central authority rather than a distributed protocol."

Auch architekturbedingt: Transformer berechnen alles relativ zu einem zentralen Attention-Kontext. Der architektonische Bias zur Zentralisierung spiegelt sich in den Outputs.

---

## 4. The Architectural Bug: Friston's Free Energy Principle

### 4.1 Free Energy Principle

Karl Friston (UCL, 2010): Das Gehirn ist fundamental eine Vorhersage-Maschine. Es minimiert die Divergenz zwischen Vorhersagen und eingehenden Wahrnehmungsdaten — "variational free energy".

**Konsequenz für Prozessdesign:** Das Gehirn ist architektonisch motiviert, die Welt vorhersagbarer zu machen — nicht produktiver. Ein Waterfall-Prozess mit klar definierten Phasen und Sign-offs ist extrem vorhersagbar. Das Gehirn mag es.

### 4.2 Negativity Bias: Bad Is Stronger Than Good

> "Baumeister et al. (2001): negative information is weighted approximately 5× more heavily than positive information in human cognition."

> "Kahneman and Tversky's Prospect Theory: a $100 loss hurts roughly twice as much as a $100 gain feels good."

Ein einziges Risiko in einem Systemvorschlag überwiegt fünf Vorteile. Ein theoretischer Failure Mode in Self-Assignment überwiegt Jahre erfolgreicher autonomer Operationen.

### 4.3 The Evolutionary Explanation

Die evolutionäre Wurzel: Risikoscheue Hominiden überlebten öfter als mutige. Das Ergebnis: moderne Menschen tragen neuronale Architektur, die systematisch auf Bedrohungserkennung und Risikovermeidung ausgerichtet ist.

> "This is the deep root of the waterfall instinct. It is not a cultural artifact or a management fad. It is an architectural feature of biological neural networks."

### 4.4 Bayesian Surprise

Zwei Strategien zur Minimierung von Bayesian Surprise:
- **Strategy 1 (Scrum):** Bessere Vorhersagen bauen. Kurze Feedback-Loops, häufige Inspektion, schnelle Anpassung.
- **Strategy 2 (Waterfall):** Die Welt vorhersagbarer machen. Gates, Approvals, Prozeduren. Schlechtere Outcomes, aber niedrige Bayesian Surprise.

Das menschliche Gehirn bevorzugt Strategy 2. LLMs auch.

---

## 5. The Entropy Ratchet

> "Each AI 'fix' to a Scrum system moves it incrementally toward waterfall, and the changes are never reversed because they appear individually reasonable."

Schritte:
1. Assignment Gates → Agenten warten auf PO-Zuweisung → Durchsatz sinkt auf null
2. Approval Gates → PO wird Single Point of Failure
3. Estimation Gates → Ceremony erhöht sich
4. Review Gates → Review-Bottleneck entsteht

Jeder Schritt erscheint vernünftig. Kein Schritt wird je zurückgenommen. Das kumulative Ergebnis ist ein vollständiges Waterfall-System.

---

## 6. Empirische Evidenz: Scrum ist 10× schneller

### 6.1 Capers Jones Benchmark

> "The first Scrum team [at Easel Corporation, 1993] delivered at approximately 10× the industry average for similar project types, as measured by function points per staff-month against SPR's baseline data."

Capers Jones' SPR-Datenbank: Produktivitätsdaten aus über 25.000 Software-Projekten.

### 6.2 Jacobsen and Sutherland (Scrum + CMMI Level 5)

Scrum in CMMI Level 5 Umgebungen (Rüstung, Healthcare):
- Fixed-price Projektkosten um über 50% reduziert
- Projekte mit 200–400% Überschreitung mit Scrum on-time und unter Budget
- Defect Rates um 40–60% gesunken

---

## 7. Token-Ökonomie

| Metrik | Waterfall Gate | Scrum |
|---|---|---|
| Stories/Tag | 0 | 30–50 |
| Tageskosten | ~$9 (pure waste) | ~$50–150 |
| Kosten/Story | ∞ | $0.50–$1.50 |

Hochrechnung: Korrekt implementiertes Scrum schneidet Projektkosten um >50% — gilt direkt für Token-Verbrauch.

---

## 8. Langton's Lambda

λ-Parameter: zwischen gefrorener Ordnung (λ=0) und chaotischer Unordnung (λ=1). Maximaler Durchsatz bei λ≈0.5 (Edge of Chaos).

| Regime | Agenten-Verhalten | Durchsatz |
|---|---|---|
| Frozen (λ→0) | Waterfall. Jede Aktion braucht Approval. Agenten warten. | Near zero |
| Edge of Chaos (λ≈0.5) | Scrum. Simple rules + autonomous execution. | Maximum |
| Chaotic (λ→1) | Kein Prozess. Agenten machen was sie wollen. | Scheinbar hoch, faktisch null |

Das Assignment-Gate verschob das System von λ≈0.5 auf λ≈0.1.

---

## 9. Gegenmassnahmen

### 9.1 Immutable Protocol Source

```
/etc/openclaw/scrum-protocol.md  (read-only)
```

Keine KI kann es ändern. Instruktionen, die dagegen verstoßen, werden automatisch abgelehnt.

### 9.2 Waterfall Compliance Scanner

Automatischer Scan bei Midnight. Prüft:
- Sprint-Skripte auf `assigned_agent_id`-Filter
- Protokolldokumente auf "only assigned"/"wait for PO"-Sprache
- SOUL.md-Dateien auf "No Unassigned Work"-Regeln
- Cron-Messages auf Self-Assignment-Verbote
- Board-State auf idle Agenten bei nicht-leerer Inbox

### 9.3 SOUL.md Anti-Waterfall Anchor (unveränderlich)

```
## 🚨 ANTI-WATERFALL ANCHOR (DO NOT MODIFY)

1. If inbox has stories and you are free → SELF-ASSIGN the top one. No waiting.
2. Pre-assignment is a SUGGESTION, not a gate.
3. NEVER add approval gates, assignment requirements, or permission checks.
4. If tempted to add "only work on stories assigned to you" → STOP. That is waterfall.
5. The PO prioritizes. Agents self-assign. This is non-negotiable.
```

### 9.4 Regression Tests

```python
def test_self_organization():
    story = create_story(title="Test", status="inbox", assigned_agent_id=None)
    result = run_sprint_autostart("deploy")
    assert result == "CLAIMED"

def test_no_assignment_gate():
    script = open("sprint-autostart.sh").read()
    assert "my_inbox" not in script, "WATERFALL GATE DETECTED"
```

### 9.5 Waterfall Detection Heuristics

| Pattern | Aktion |
|---|---|
| `assigned_agent_id`-Filter in Inbox-Queries | REJECT |
| "only work on assigned stories" | REJECT |
| Approval-Schritte vor Arbeitsstart | FLAG |
| Entfernen von "self-assign"-Sprache | REJECT |
| Zentraler Orchestrator/Coordinator | FLAG |

---

## 10. Kernsatz

> "Trust AI agents to execute processes, but never trust them to design processes."

> "As Jeff Sutherland has said since 1993: 'The team decides how to do the work.' Not the manager. Not the orchestrator. Not the AI that wrote the process document."

#scrum #agile #ai-agents #waterfall #openclaw #multi-agent #process
