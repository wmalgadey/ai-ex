---
URL: https://meditations.metavert.io/p/resurrecting-a-1992-mud-with-agentic
Gespeichert: 2026-04-09
---

# Resurrecting a 1992 MUD with Agentic AI

_Jon Radoff, metavert.io_

MUD "Legends of Future Past" (1992, CompuServe) — 7 Jahre online, 27 Jahre tot — an einem Wochenende mit Claude Code wiederhergestellt. Ohne Quellcode.

## Was vorhanden war

- Script-Dateien in einer selbst erfundenen Sprache (1990er DOS-Encoding)
- Gameplay-Aufzeichnung von 1996
- GM-Scripting-Manual von 1998
- Kein Game Engine Source Code

## Was Claude Code daraus machte

> "A game that I originally coded over six months—with a team of Game Masters building the content over years—came back to life in a weekend of agentic engineering."

- Reverse-engineered die proprietäre Scripting-Sprache (IFVERB, IFVAR, IFITEM, etc.)
- Decoded Kampfformeln aus GM-Dokumentation
- Inferierte Monster-KI-Profile aus Integer-Feldern
- Baute eine vollständige Game Engine in Go, React Frontend, WebSocket-Multiplayer, MongoDB-Persistenz
- Deploy auf Fly.io

Ergebnis: 2.273 Räume, 1.990 Items, 297 Monster-Typen, 88 Zaubersprüche, 5 Magieschulen, Crafting-System, 8 Rassen.

## Kernaussage

> "The engineering was handled by an AI agent. My job was to provide the creative artifacts and to make judgment calls the agent couldn't make on its own. The imagination was the input. The implementation was automated."

Verweis auf Vernor Vinge's "programmer-archaeologist" aus *A Deepness in the Sky* — Vinge hat 1999 beschrieben was 2026 Realität wird.

## Links

- [Artikel](https://meditations.metavert.io/p/resurrecting-a-1992-mud-with-agentic)
- [Spiel live](https://lofp.metavert.io/)
- [GitHub (MIT)](https://github.com/jonradoff/lofp)

#agentic-engineering #claude-code #software-archaeology #reverse-engineering #game-dev
