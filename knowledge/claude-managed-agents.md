---
URL: https://claude.com/blog/claude-managed-agents
Gespeichert: 2026-04-09
---

# Claude Managed Agents

_8. April 2026 — Public Beta_

Anthropic launcht Claude Managed Agents: Suite von APIs für cloud-gehostete Agents auf Anthropic-Infrastruktur.

> "Building agents meant spending development cycles on secure infrastructure, state management, permissioning, and reworking your agent loops for every model upgrade."

Das soll wegfallen. Was enthalten ist:

- **Secure Sandboxing** — Code Execution, Auth, Tool-Handling durch Anthropic verwaltet
- **Long-running Sessions** — Stunden autonomer Arbeit, persistent auch bei Verbindungsabbruch
- **Multi-agent Coordination** — Agents spawnen und koordinieren andere Agents (Research Preview)
- **Trusted Governance** — Scoped Permissions, Identity Management, Execution Tracing

Pricing: Standard Token-Rates + **$0.08 pro Session-Hour** aktive Runtime.

## Einstieg

- [Docs](https://platform.claude.com/docs/en/managed-agents/overview)
- [Console Quickstart](https://platform.claude.com/workspaces/default/agent-quickstart)
- Claude Code: `"start onboarding for managed agents in Claude API"`

> **TODO: Kurs/Onboarding abschließen** — Claude Code built-in Skill `claude-api` nutzen

#claude #anthropic #managed-agents #agentic #platform
