# Von OpenClaw zu NanoClaw — Eine persönliche Journey

**Gespeichert:** 2026-03-22

## Ausgangslage

OpenClaw war der Einstieg. Das Projekt hat beeindruckt — ein vollständiger KI-Assistent, multi-channel, aktive Community. Aber je länger man damit arbeitet, desto klarer wird: Es ist zu viel. Zu viele Features, zu viele lose Teile, zu viel Code.

Das eigentliche Ziel war nicht, einen fertig konfigurierten Assistenten zu haben. Es war, KI nutzen zu lernen — zu verstehen wie diese Systeme funktionieren, was möglich ist, wo die Grenzen liegen. Und OpenClaw steht diesem Ziel im Weg.

## Der Bruch: Update 2026.3.2

Der konkrete Auslöser war ein OpenClaw-Update im März 2026. Version 2026.3.2 aktivierte automatisch neue Security-Funktionen — ohne dass klar kommuniziert wurde, was sich ändert und wie man damit umgeht. Danach funktionierte der eigene Assistent nicht mehr wie gewohnt.

Was folgte, war der typische OpenClaw-Debugging-Albtraum:

- **Tausende Commits und PRs** im Repo, davon ein verschwindend kleiner Teil relevant für das eigene Problem
- **Dokumentation, die dem Code hinterherhinkt** — die dokumentierten Lösungsschritte funktionierten schlicht nicht
- **KI-generierte Doku** in rauen Mengen: so viel Text, dass kein Mensch ihn lesen kann, geschweige denn will

Das Security-Problem vom Update 2026.3.2 ist bis heute nicht verstanden. Das System wurde einfach ersetzt.

## Was NanoClaw anders macht

NanoClaw hat einen fundamental anderen Ansatz — und der passt besser:

**Klein genug zum Verstehen.** Der gesamte Codebase passt in wenige Dateien. Wenn etwas nicht funktioniert, kann man nachschauen warum. Kein Rätselraten.

**KI-zentrisch, nicht KI-garniert.** NanoClaw nutzt den Claude Agent SDK direkt. Die KI ist nicht ein Feature unter vielen — sie ist das Werkzeug, mit dem das System konfiguriert, erweitert und debuggt wird. Das ist der Ansatz, mit dem man KI wirklich lernt.

**Features als Skills, nicht als Codebase-Ballast.** Neue Funktionen kommen als Skills — eigenständige, verstehbare Einheiten. Man installiert was man braucht, nicht was irgendjemand sonst für nützlich hält.

**Sicherheit durch Isolation, nicht durch Application-Layer.** Agents laufen in eigenen Containern. Das ist strukturell sicher, nicht durch Checklisten und Pairing Codes.

## Fazit

Der Wechsel von OpenClaw zu NanoClaw war kein Feature-Vergleich. Es war eine Entscheidung darüber, welcher Ansatz zum eigentlichen Lernziel passt. Wer KI verstehen will, braucht ein System das man verstehen kann — nicht eines, das für einen denkt.

## Tags

#nanoclaw #openclaw #personal #journey #ai-tools #vibe-coding
