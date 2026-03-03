# Claude Code Best Practice

**Source:** https://github.com/shanraisshan/claude-code-best-practice  
**Author:** Shan Raisshan (shanraisshan)  
**Tagline:** "practice makes claude perfect"

## Feature Map

| Feature | Location | Description |
|---|---|---|
| Commands | `.claude/commands/<name>.md` | Entry-point prompts for workflows — invoke with `/command-name` |
| Sub-Agents | `.claude/agents/<name>.md` | Custom agents with own name, color, tools, permissions, model |
| Skills | `.claude/skills/<name>/SKILL.md` | Reusable knowledge/workflows — load on-demand or invoke with `/skill-name` |
| Hooks | `.claude/hooks/` | Deterministic scripts outside agentic loop on specific events |
| MCP Servers | `.claude/settings.json`, `.mcp.json` | Connections to external tools, databases, APIs |
| Plugins | distributable packages | Bundles of skills, subagents, hooks, MCP servers |
| Settings | `.claude/settings.json` | Hierarchical config — permissions, model, output styles, sandboxing |
| Memory | `CLAUDE.md`, `~/.claude/projects/<project>/memory/` | Persistent context via CLAUDE.md + `@path` imports |
| Checkpointing | automatic (git-based) | Tracks file edits — rewind with Esc Esc or `/rewind` |

## Orchestration Pattern: Command → Agent → Skill

```
claude /weather-orchestrator
       └── weather-agent (Agent with preloaded skill)
               └── weather-fetcher (Skill: fetches data)
               └── weather-svg-creator (Skill: creates output)
```

## Best Practices — Workflows

- `CLAUDE.md` should not exceed 150 lines (60 is better)
- Use **commands** for workflows, not agents (agents = extra context, not entry points)
- Feature-specific subagents with skills (progressive disclosure) instead of generic "qa agent"
- `/memory`, `/rules`, `constitution.md` do not guarantee behavior
- Avoid "agent dumb zone" — manual `/compact` at max 50% context
- Always start with **plan mode**
- Vanilla Claude Code is better than complex workflows for smaller tasks
- Commit often — as soon as a task is completed
- **Agent teams + git worktrees** for parallel development
- Use **Ralph Wiggum plugin** for long-running autonomous tasks

## Best Practices — Utilities

- iTerm (not IDE) to avoid crash issues
- Wispr Flow for voice prompting
- claude-code-voice-hooks for audio feedback
- Status line for context awareness + fast compacting
- Use `/permissions` with wildcard syntax (`Bash(npm run *)`, `Edit(/docs/**)`) instead of `dangerously-skip-permissions`
- `/sandbox` to reduce permission prompts (file + network isolation)
- Output styles: **Explanatory** when learning new codebase, **Learning** for coaching

## Best Practices — Debugging

- `/doctor`
- Run terminals as background tasks for better log visibility
- Use MCP (Claude in Chrome, Playwright, Chrome DevTools) to let Claude see console logs
- Provide screenshots of the issue

## Reports in the Repo

| Report | Description |
|---|---|
| Agent SDK vs CLI System Prompts | Why CLI and Agent SDK outputs differ |
| Browser Automation MCP Comparison | Playwright vs Chrome DevTools vs Claude in Chrome |
| Global vs Project Settings | What's global-only (~/.claude/) vs dual-scope |
| Skills Discovery in Monorepos | How skills are discovered in large monorepos |
| Agent Memory Frontmatter | Persistent memory scopes (user, project, local) for subagents |
| Advanced Tool Use Patterns | PTC, Tool Search, Tool Use Examples |
| Usage, Rate Limits & Extra Usage | `/usage`, `/extra-usage`, `/cost`, rate limits, pay-as-you-go |

## Claude Killed / Alternatives Noted

| Claude Feature | Alternatives |
|---|---|
| Voice Mode | Wispr Flow, SuperWhisper |
| Remote Control | **OpenClaw** |
| Cowork | OpenAI Operator, AgentShadow |
| Tasks | Beads |
| Skills/Plugins | YC AI wrapper startups |

## Links

- Boris Cherny tips (Jan–Feb 2026): https://x.com/bcherny/status/2007179832300581177
- Ralph Wiggum plugin: https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum
- claude-code-voice-hooks: https://github.com/shanraisshan/claude-code-voice-hooks
- claude-code-status-line: https://github.com/shanraisshan/claude-code-status-line
