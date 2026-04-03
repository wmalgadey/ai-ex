---
URL: https://www.patreon.com/posts/1st-claude-app-w-151644630
Gespeichert: 2026-03-01
---

# Alistair Cockburn – 1st Claude App with Hexagonal Architecture


## Was ist das?

Alistair Cockburn (Erfinder der Hexagonal Architecture / Ports & Adapters) dokumentiert auf Patreon wie er mit Claude eine App entwickelt — als Live-Protokoll des Entwicklungsprozesses.

## Links
- Patreon-Post: https://www.patreon.com/posts/1st-claude-app-w-151644630
- Alistair Cockburn: https://alistair.cockburn.us
- Hexagonal Architecture: https://alistair.cockburn.us/hexagonal-architecture/

## Verwandte Ressourcen

### Claude Code Command: Hexagonal Architecture (Romilly Riddle)
**Quelle:** https://github.com/romilly/claude-code-helpers/blob/main/resources/commands/hexagonal.md

Kompakter Claude-Prompt/Command der Hexagonal Architecture + Walking Skeleton für Claude Code umsetzt:

- Domain logic: unabhängig von I/O, Persistence, externen Systemen
- Ports: Abstrakte Interfaces (Python ABCs)
- Adapters: Implementierungen (fake, real)
- **Walking Skeleton:** Erst Use Case definieren (Cockburn-Stil: System, Actor, Goal, Scenarios), dann minimal end-to-end mit Fake Adapters
- **Testing:** Keine Monkeypatching — explizite Dependency Injection mit ABCs + Contract Tests

```
src/project_name/
├── domain/     # Pure business logic, no I/O
├── ports/      # Abstract interfaces (ABCs)
└── adapters/   # Implementations (fake, real)
```

_Patreon erfordert Login — direkter Fetch nicht möglich._

#hexagonal-architecture #ports-and-adapters #claude #ai-development #alistair-cockburn
