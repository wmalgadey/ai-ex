---
URL: https://github.com/IyadhKhalfallah/clauditor
Gespeichert: 2026-04-11
---

# clauditor

Claude Code Session-Optimizer: Überwacht Token-Waste und rotiert Sessions automatisch bevor die Quota verbrennt.

## Problem

Jeder Claude Code Turn re-sendet die komplette Konversationshistorie:

```
Turn   1: ██          20k tokens/turn
Turn  50: ██████████  100k tokens/turn
Turn 200: ████████████████████  200k tokens/turn
```

Nach 200 Turns sendet jeder Turn 10× mehr als nötig — gleiche Arbeit, 10× mehr Quota.

## Was clauditor macht

Registriert 7 Hooks in Claude Code und blockt die Session wenn der Waste-Faktor zu hoch ist:

> "clauditor: Session using 9x more quota than necessary. Your progress has been saved. Run `claude` to start a fresh session."

- **Waste Factor** = current tokens/turn ÷ baseline tokens/turn — ab 10× wird geblockt
- Speichert Session-Context (strukturiertes Handoff-Template + mechanisch extrahierte Daten)
- Neues Session: `"continue"` → clauditor zeigt gespeicherte Sessions + copy-pastebare Prompts
- Erkennt bekannte Cache-Bugs (Claude Code 2.1.69–2.1.89: 10-20× Token-Verbrauch)

## Install

```bash
brew install IyadhKhalfallah/clauditor/clauditor
clauditor install
# oder:
npm install -g @iyadhk/clauditor && clauditor install
```

## Zahlen (reale Nutzung, 37 Sessions)

- 15 von 37 Sessions brannten 5× mehr Quota als nötig
- Mit Rotation: **157M statt 418M Tokens (62% Ersparnis)**

## Read-only Modus (keine Hooks)

```bash
clauditor report    # Waste-Übersicht
clauditor sessions  # per-Session-Breakdown
clauditor doctor    # Cache-Bug-Scan
clauditor time      # Token-Kosten nach Tageszeit
```

#claude-code #quota #token-optimization #tooling
