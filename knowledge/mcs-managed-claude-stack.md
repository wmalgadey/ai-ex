# mcs — Managed Claude Stack

**URL:** https://github.com/bguidolim/mcs
**Gespeichert:** 2026-03-17
**Sprache:** Swift (macOS 13+)
**Lizenz:** MIT
**Version:** 2026.3.17

## Was ist das?

`mcs` ist ein macOS CLI-Tool, das Claude Code-Konfigurationen portabel und reproduzierbar macht. Das Problem: MCP-Server, Plugins, Hooks, Skills, Slash-Commands und Settings müssen auf jedem neuen Rechner oder im Team manuell neu eingerichtet werden. `mcs` löst das durch **Tech Packs** — Git-Repos mit einer `techpack.yaml`, die alles deklarativ beschreibt. Ein `mcs sync` installiert alles konsistent.

## Kernkonzept: Tech Packs

Ein Tech Pack ist ein Git-Repository mit einer `techpack.yaml`. Unterstützte Komponenten:

| Typ | Beschreibung |
|---|---|
| `brew:` | Homebrew-Paket als Abhängigkeit |
| `mcp:` | MCP-Server (stdio oder HTTP) |
| `plugin:` | Claude Code Plugin |
| `hook:` | Lifecycle-Hook (SessionStart, UserPromptSubmit, etc.) |
| `command:` | Slash-Command (.md-Datei) |
| `skill:` | Skills-Verzeichnis |
| `agent:` | Subagent |
| `settingsMerge:` | Settings-JSON merge |
| `gitignore:` | Gitignore-Einträge |

**Prompts** in der YAML erlauben interaktive Wertabfragen beim Sync (`fileDetect`, `input`, `select`, `script`). Werte werden als Placeholder in alle Configs substituiert — gut für API-Keys und projektspezifische Einstellungen.

**Dependencies** zwischen Komponenten sind möglich, auch cross-pack. Topologische Sortierung mit Zykluserkennung.

## Die fünf Befehle

**`mcs sync [path]`** — Hauptbefehl. Interaktive Auswahl welche Packs aktiv sein sollen, Diff berechnen, Templates auflösen, installieren. Mit `--global` für `~/.claude/`, `--dry-run` zum Vorschauen.

**`mcs pack add/remove/list/update`** — Lokale Pack-Registry verwalten. Quellen: Git-URL, GitHub-Shorthand (`user/repo`), lokaler Pfad.

**`mcs doctor [--fix]`** — Health-Check in 5 Schichten (auto-abgeleitete, komponenten-, pack-, cross-component- und projektweite Checks). Mit `--fix` automatische Reparaturen.

**`mcs export [outputDir]`** — Liest bestehende live Claude-Konfiguration und generiert daraus eine `techpack.yaml`. Sensitive Env-Variablen werden durch Placeholder ersetzt.

**`mcs cleanup`** — Löscht timestamped Backup-Dateien.

## Sync-Flow (vereinfacht)

1. Multi-select: welche Packs sollen konfiguriert werden
2. Diff berechnen (neu / entfernt)
3. Template-Werte auflösen (inkl. Prompts)
4. Deselektierte Packs bereinigen
5. Globale Dependencies installieren (brew, plugins)
6. Pro-Projekt-Artefakte mit Placeholder-Substitution installieren
7. `settings.local.json` aus allen Hook-Einträgen komponieren
8. `CLAUDE.local.md` aus Template-Sektionen zusammensetzen (via `<!-- mcs:begin/end -->` Marker)
9. Gitignore-Einträge setzen
10. Lockfile schreiben (`mcs.lock.yaml`)

## Safety & Trust

- **Backups** vor jeder Dateimodifikation (timestamped, `mcs cleanup` zum Aufräumen)
- **SHA-256-Verifikation** aller Skripte aus externen Packs
- **Idempotent** — beliebig oft wiederholbar
- **Non-destructive** — User-Content außerhalb der `<!-- mcs:begin/end -->`-Marker bleibt unberührt
- **Path Containment Checks** gegen Directory-Traversal
- **Lockfile** für reproduzierbare Builds (gepinnte Commits)

## Technisches

Swift 6, strict concurrency. Zwei externe Dependencies: `swift-argument-parser` (Apple CLI-Framework), `Yams` (YAML-Parsing). Aktives Projekt mit 14 Releases seit Ende Februar 2026.

## Vergleich zu NanoClaw Skills

NanoClaw-Skills sind Branch-basiert und Code-Merge-orientiert — man zieht sich einen Branch rein und hat den Code. `mcs` ist deklarativ und betriebssystem-agnostisch zur Konfiguration: kein Code, nur YAML + Markdown. Die Zielgruppen überschneiden sich (Reproduzierbarkeit von Claude-Setups), der Ansatz ist grundlegend verschieden.

## Tags

#claude-code #cli #devtools #macos #swift #mcp #configuration #tech-packs
