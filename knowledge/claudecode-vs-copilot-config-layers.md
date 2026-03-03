# Claude Code vs. GitHub Copilot — Config Layers (6 Layers)

**Source:** https://www.linkedin.com/posts/joshua-dell_aicoding-claudecode-githubcopilot-share-7434064377323884544-Ksxg  
**Author:** Joshua Dell  
**Date:** 2026-03-02

## Overview

Comparison of how Claude Code and GitHub Copilot map to each other across repo-level configuration — 6 layers.

## The 6 Layers

### 1. Repo Memory
- **Claude:** `CLAUDE.md` in project root
- **Copilot:** `.github/copilot-instructions.md`
- Both load automatically every session. VS Code also supports `AGENTS.md` as a cross-tool standard.

### 2. Scoped Instructions
- **Claude:** `.claude/rules/` with glob-based paths frontmatter
- **Copilot:** `.github/instructions/*.instructions.md` with `applyTo` glob patterns
- Both let you give the model different rules for different parts of the codebase.

### 3. Reusable Skills & Commands
- **Claude:** `.claude/skills/` — auto-discovered, invoked via `/skill-name`
- **Copilot:** Agent Skills (`.github/skills/SKILL.md`) for multi-step workflows + Prompt Files (`.github/prompts/*.prompt.md`) as /slash-commands
- Claude unifies skills and slash commands. Copilot separates them — skills are heavier, prompt files are lighter.

### 4. Guardrail Hooks
- **Claude:** `.claude/settings.json` hooks — deterministic pre/post actions
- **Copilot:** `.github/hooks/*.json` — `preToolUse`, `postToolUse`, `sessionStart`
- Not probabilistic. They fire every time, no exceptions.

### 5. Docs on Demand
- Both: Keep instruction files lean — link to a `docs/` folder for ADRs, runbooks, and architecture. The model reads them when it needs context, not all at once.

### 6. Extensibility
- **Claude:** `/plugin install` from official + community marketplaces, plus MCP servers for external tools via an open protocol
- **Copilot CLI:** Two built-in plugin marketplaces, community plugins from GitHub repos or local directories

## Cross-Tool Convergence

- VS Code reads `.claude/skills/`, `.claude/rules/`, and `CLAUDE.md`
- Copilot's coding agent supports `AGENTS.md` natively
- Claude Code doesn't read `AGENTS.md` yet → workaround: symlink to `CLAUDE.md` or use `@AGENTS.md` imports
- Same hook event names across both tools
- MCP is an open protocol → one repo can serve multiple AI tools

## Resources

- Awesome GitHub Copilot: https://lnkd.in/ep2tAsek
- Awesome Claude Code: https://lnkd.in/eT3bqD9D
- Copilot CLI Plugins: https://lnkd.in/eSZSJ53T
- Claude Code MCP: https://lnkd.in/eKBiDJxs
- Claude Code Plugins: https://lnkd.in/eaEwCg2Z
