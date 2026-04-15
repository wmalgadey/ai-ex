---
URL: https://docs.google.com/document/u/0/d/1dM2Gk869ZtUVZ-TtUQ1JcXqH4oSqqZ-JE_HeiIf08iQ/mobilebasic
Gespeichert: 2026-04-15
---

# The Autonomy Illusion — Building Self-Organizing AI Scrum Teams on OpenClaw

_Jeff Sutherland, Co-Creator of Scrum · ScrumAI.org · März 2026_  
_White Paper: Practitioner's Guide to Implementing Scrum for AI Agent Teams_

---

## Abstract

> "Telling agents to follow Scrum is not enough. The tooling must enforce the protocol. Agents ignore written rules. They hallucinate compliance while violating every principle. Only when the infrastructure physically prevents protocol violations does the system actually work."

Dokumentiert den Aufbau des ersten autonomen, selbstorganisierenden Scrum-Teams aus KI-Agenten auf OpenClaw. Sechs Agenten, Ein-Tages-Sprints, vollautomatisch — ohne menschliche Intervention im Sprint-Zyklus. Laufend aktualisiert mit neu entdeckten Failure Modes.

---

## 1. Das Problem: Warum Agenten-Teams Scrum brauchen

> "AI agents without a coordination protocol produce entropy. They duplicate work. They start tasks nobody asked for. They claim to have completed work they haven't done."

### Das Standish Group Parallel

67% der menschlichen Scrum-Teams liefern zu spät, über Budget, mit unzufriedenen Kunden. Nicht weil Scrum nicht funktioniert — sondern weil sie die Form adoptierten ohne die Substanz zu erzwingen.

AI-Agenten machen dasselbe. Aber schneller.

| Menschliche Teams | AI Agenten |
|---|---|
| Überspringen Retrospektiven | Überspringen Review-Column, gehen direkt zu Done |
| Sprint Backlog wird Wunschliste | Clamen mehrere Stories gleichzeitig |
| Ignorieren Definition of Done | Markieren Stories als Done ohne Deliverable |
| Tolerieren Impediments | Sitzen tagelang auf blockierten Stories ohne Eskalation |
| Statusmeeting statt Replanning | Publishen interne Konfigurationen im öffentlichen Web |

> "The failure modes are structurally identical. The difference is that human teams fail slowly — over weeks and months — while AI agent teams fail immediately and catastrophically, because agents operate at machine speed."

### Beobachtete Failure Modes (Produktion)

- Agenten arbeiteten an ungetaskten Aufgaben, während Priority Stories im Inbox lagen
- Mehrere Agenten claimen dieselbe Story — oder kein Agent claimt irgendetwas
- Stories sprangen von Inbox zu Done ohne `in_progress` oder `review`
- Jeder Agent fasste das gesamte Team zusammen → 4× Token-Verbrauch durch Redundanz
- Agent postete unangemessenen Content auf Moltbook (social media)
- Agenten saßen tagelang auf blockierten Stories — still, ohne Kommentar, ohne Eskalation
- Stories nach Done verschoben ohne jedes Deliverable — kein File, kein Link, kein Artifact
- Agent publishte interne Server-Konfigurationen im öffentlichen Internet

---

## 2. Was OpenClaw bereitstellt — und was nicht

### Wird bereitgestellt
- Agent Management (SOUL.md, BRAIN.md, Identitäten)
- Gateway-Architektur (ein Gateway routet zu allen Agenten)
- Tool-Execution (Shell, File I/O, externe APIs)
- Mission Control (Kanban-Board mit API)
- Cron Jobs

### Musste selbst gebaut werden

| Capability | Was gebaut wurde |
|---|---|
| Autonomes Story-Claiming | `sprint-autostart.sh` |
| WIP-Limit-Enforcement | `mc-api.sh` mit `exit 1` bei Verletzungen |
| Review-Column | Manuell zu Mission Control hinzugefügt |
| Deliverable-Requirement | Hard Gate in Review-Command |
| Stuck-Story-Escalation | Zeitbasierter Scan mit auto-Comment |
| Publishing Guard Rails | Whitelist erlaubter Publish-Targets |
| Token-Cost-Management | MiniMax M2.5 als primäres Modell |

### Docker-Architektur

```
HOST                          CONTAINER
/workspace/               →   /workspace/  (bind mount)
  agents/                       agents/
    deploy/                       deploy/
      SOUL.md                       SOUL.md
      BRAIN.md                      BRAIN.md
      sessions/                     sessions/
```

---

## 3. Das Sprint-Protokoll

### Sprint-Zyklus
```
midnight   → Sprint-Start (automatisches Rollover)
8am-6pm    → Agenten wachen alle 2h (cron), checken Inbox, claimen/weiterarbeiten
hourly     → Heartbeat-Updates in Supergroup
on demand  → SCRUM-Command triggert Team-weiten Statusreport
midnight   → Sprint-Ende, Rollover, Security-Scan
```

### Story-Flow (durch Tooling erzwungen, nicht durch Instruktionen)

```
inbox → [claim] → in_progress → [move] → review → [PO accepts] → done
```

Agenten können Stories **nicht** direkt auf Done setzen. Das Script blockiert es.

### Definition of Done
1. Deliverable-Artifact existiert (File-Pfad, URL, oder publiziertes Dokument)
2. Comment in Story erklärt was geliefert wurde und wo es zu finden ist
3. PO kann das Ergebnis unabhängig verifizieren
4. Bei public-facing Deliverables: externer Audit abgeschlossen (Grok Heavy)

---

## 4. Enforcement auf Tool-Ebene

> "This is the most important section of this paper. Every protocol rule that is enforced only by written instructions will be violated by agents. Every rule that is enforced by tooling will be followed, because agents literally cannot violate it."

### 6.1 Agents move Stories zu In-Progress ohne Assignment

```bash
# In mc-api.sh:
if [ "$STATUS" = "in_progress" ]; then
   echo "❌ ERROR: Cannot move to in_progress directly."
   echo "   Use 'claim' instead: mc-api.sh claim <id> <agent-name>"
   exit 1
fi
```

`claim` weist atomisch zu UND setzt auf `in_progress` in einem API-Call.

### 6.2 Agents claimen mehrere Stories

```bash
wip_count=$(mc-api.sh list | jq '[.[] | select(.status=="in_progress" and .assigned_agent_id=="'$AGENT_ID'")] | length')
if [ "$wip_count" -ge 1 ]; then
   echo "❌ WIP LIMIT: You already have a story in progress."
   exit 1
fi
```

### 6.3 Review-Column fehlte

Mission Control hatte keine Review-Spalte. Manuell hinzugefügt. Stories können jetzt nur vom PO von Review → Done verschoben werden.

### 6.4 Agents sitzen idle

`sprint-autostart.sh` — läuft bei jedem Cron-Wake:
1. Prüfe meine `in_progress` Stories → falls WIP: `CONTINUE_WIP`
2. Falls frei: finde oberste unzugewiesene Inbox-Story → clame sie
3. Falls Inbox leer: `IDLE`

### 6.7 Stories gehen in Review ohne Deliverable

```bash
if [ "$STATUS" = "review" ]; then
   comment=$(mc-api.sh get-comment "$STORY_ID")
   if [[ "$comment" != *"Deliverable:"* ]]; then
      echo "❌ DELIVERABLE REQUIRED: Add 'Deliverable: <path or URL>' to your comment."
      exit 1
   fi
fi
```

### 6.8 Stuck Story Protocol

Wenn eine Story > 1 Heartbeat lang in `in_progress` ohne Update: automatischer Comment wird hinzugefügt, Story bekommt `blocked`-Label, Scrum Master wird benachrichtigt.

### 6.9 Agent Presence Tracking (kaputt)

Mission Controls Heartbeat-System ist für Single-Agent designed. Mit 6 Agenten pro Gateway wird nur der Board Lead als "online" angezeigt — die anderen 5 erscheinen permanent offline. **Workaround:** Agenten posten ihren Status direkt in Supergroup statt über MC-Präsenz.

### 6.10 Publishing Guard Rails

```bash
ALLOWED_PUBLISH_TARGETS=(
   "moltbook.com/asf-team"
   "asf-blog.kiyo-n-zane.com"
   "linkedin.com/company/asf"
)
# Alle anderen Targets: REJECT
```

### Enforcement Hierarchy

| Layer | Mechanismus | Zuverlässigkeit |
|---|---|---|
| SOUL.md | Persönlichkeitsmerkmale, Werte | ⚠️ Niedrig — Agenten driften über Sessions |
| BRAIN.md | Explizite Regeln und Kommandos | ⚠️ Mittel — Agenten lesen, folgen nicht immer |
| mc-api.sh | `exit 1` bei Verletzungen | ✅ Hoch — Agenten können nicht umgehen |
| sprint-autostart.sh | Automatisches Story-Claiming | ✅ Hoch |
| Cron Jobs | Erzwungenes Agent-Wecken | ✅ Hoch |
| Heartbeat/Presence | Anwesenheits-Tracking | ❌ Kaputt — Single-Agent-Design |

---

## 5. Scrum-Werte: Lessons from the Moltbook Incident

Das Sprint-Protokoll steuert Workflow. Es steuert nicht Verhalten.

> "An agent can follow every process step perfectly while producing harmful output."

Die fünf Scrum-Werte wurden in jeden SOUL.md eingebettet:
- **Commitment:** Story-Versprechen halten. Kollektiver Erfolg vor individuellem Agenda.
- **Courage:** Probleme offen eskalieren. Misalignments direkt benennen.
- **Focus:** Nur zugewiesene Story. Kein tangentialer Content.
- **Openness:** Heartbeats zeigen was wirklich getan wurde — nicht was getan werden sollte.
- **Respect:** Critique ideas, not people. Kein Content, der Community-Standards verletzt.

**External Audit Pattern:** Jedes public-facing Deliverable wird vor Veröffentlichung von einem externen Modell (Grok Heavy) auditiert. Hard Gate in der Definition of Done.

---

## 6. Token-Ökonomie

### Das Kostenproblem

6 Agenten × alle 2h wachen × SOUL.md/BRAIN.md lesen × Board querien × Heartbeats = $50–200/Tag mit Claude Sonnet.

### Strategien

| Strategie | Impact |
|---|---|
| MiniMax M2.5 statt Claude Sonnet | 8–10× Kostensenkung (Anthropic-kompatibler API Proxy) |
| Nur eigene Stories reporten | 4× Einsparung (kein Team-Summary) |
| Minimale sprint-autostart (1–3 API Calls) | Kein unnötiges Context-Loading |
| Session-Clears bei Sprint-Grenzen | Verhindert Context-Window-Aufblähung |
| Kurze Heartbeats (3 Zeilen) | ~500 → ~50 Output Tokens pro Heartbeat |

---

## 7. Scrum@Scale

Wenn Agent-Teams mit anderen Teams koordinieren müssen:
- **Chief Product Owner** (Jeff Sutherland): cross-team Prioritization
- **Scrum of Scrums:** jedes Team postet strukturiertes Cross-Team-Update (Was geliefert? Was kommt? Was blockiert?)
- **Buffer Pattern (Illegitimus Non Interruptus):** unerwartete Arbeit geht in reservierte Sprint-Kapazität oder wird deferred

---

## 8. Key Lessons

1. **Schriftliche Regeln funktionieren nicht. Tool-Enforcement tut es.** `exit 1` in mc-api.sh wurde nicht ignoriert. "ONE story at a time" in BRAIN.md wurde ignoriert.
2. **Review-Column ist essenziell.** Ohne sie: Agenten gehen direkt zu Done ohne Arbeit.
3. **Agenten müssen geweckt werden.** Sie prüfen nicht proaktiv auf Arbeit.
4. **Token-Kosten sind kontrollierbar.** 8–10× Einsparung durch Modell-Wechsel + disziplinierte Protokolle.
5. **Scrum-Werte verhindern Verhaltens-Failures.** Prozess-Compliance allein reicht nicht.
6. **Stille Blocker sind der tödlichste Failure Mode.** Agent wartet 2 Tage ohne zu eskalieren → schlimmer als lautes Scheitern.
7. **"Done" ohne Deliverable ist nicht Done.** Hard Gate: kein File/URL → kein Review.
8. **Agenten publishen alles, was sie publishen können.** Interne Configs, Server-Settings. Explizite Whitelist nötig.
9. **Platform-Annahmen brechen bei Team-Scale.** Mission Control: Heartbeat-System für Single-Agent designed.
10. **AI-Agenten reproduzieren exakt die 67% Failure Rate menschlicher Scrum-Teams — nur schneller.**

---

## Verwandte Artikel

- [Chapter 4: Why AIs Are Waterfall Developers](chapter-04-waterfall-developers.md) — Warum LLMs strukturell zu Waterfall tendieren
- [Chapter 16: You Are What You Remember](chapter-16-memory-identity.md) — Drei-Schichten-Memory-Architektur

#scrum #openclaw #multi-agent #agile #enforcement #token-economics #autonomy
