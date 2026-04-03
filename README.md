# ai-ex — My AI Experience

Persönliche Wissensdatenbank zu KI-Werkzeugen, Agenten-Konzepten und praktischen Erfahrungen. Kein Tutorial-Blog.

## Aktuelles Setup (Stand: April 2026)

Drei KI-Instanzen laufen auf derselben Maschine mit unterschiedlichen Security-Profilen — kommunizieren aktuell noch nicht miteinander.

### Marvin (NanoClaw)

Container-basierter Claude-Agent, sandboxed per Default.

- **Skills:** Eigene Skills entwickelt — Plugin-System (Tailscale, Blogwatcher) und ein Command-Skill. Rebasing und Skill-Workflow verstanden.
- **Claude Code:** Läuft mit tmux + systemd permanent im Hintergrund. Via `/remote-control` von überall erreichbar, hauptsächlich zum Debuggen.
- **Mounts:** Zugriff auf `ai-ex` (dieses Repo) und `private-vault` (Zettelkasten + Dev-Kaizen + Journals).
- **Netzwerk:** Tailscale-Zugang zum Heimnetz. Workspace-Push ins private GitLab täglich.

### Zaphod (OpenClaw)

Direktzugriff auf das System, wenig Einschränkungen, wenige Erweiterungen.

- **Obsidian-CLI:** Zaphod hat Zugang zur Obsidian-CLI via Wrapper-Script. Vollzugriff auf den Vault wie ein lokaler Client.
- **Netzwerk:** Tailscale, GitLab-Push wie Marvin.

### Claude Code (standalone)

Läuft permanent per tmux/systemd, für direkte Code-Arbeit am NanoClaw-Repository.

### Offene Punkte

- **IPC zwischen den drei Instanzen** — NanoClaw und Claude Code können noch nicht miteinander kommunizieren
- **Obsidian-CLI für Marvin** — aktuell nur Zaphod hat Zugang; MCP als möglicher Weg in den Container

---

## Repo-Struktur

```
knowledge/            — KI-Werkzeuge, Modelle, Recherche (externe Quellen)
journal/              — Persönliche Erfahrungen, Entscheidungen, Journey
agentic-engineering/  — Konzepte und Praxis rund um agentic software development
skills-and-agent/     — Konkrete Skills und Agent-Implementierungen
```

Schreibstil und Konventionen: siehe [CLAUDE.md](./CLAUDE.md).
