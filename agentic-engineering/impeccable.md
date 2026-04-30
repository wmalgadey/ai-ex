---
URL: https://github.com/pbakaus/impeccable
Gespeichert: 2026-04-30
Autor: Paul Bakaus
---

# Impeccable — Design-Skill-System für AI-Tools

Design Language und Skill-System gegen generisches KI-Frontend-Design. Für Claude Code, Cursor, OpenCode und andere AI-Harnesses.

---

> "Every LLM learned from the same generic templates. Without guidance, you get the same predictable mistakes."

Der Ansatz: 7 Referenzdateien (Typography, Color, Spacing, Motion, Interaction, Responsive, UX Writing) + 23 Commands als Skill, direkt in AI-Harnesses einbindbar.

**Commands (Auswahl):** `/audit`, `/critique`, `/polish`, `/animate`, `/colorize`, `/typeset`, `/layout`, `/delight`, `/harden`

**Anti-Pattern-Liste** explizit dokumentiert: kein Overuse von System-Fonts, kein grauer Text auf farbigen Hintergründen, keine reinen Schwarz/Grau-Werte, keine verschachtelten Card-Strukturen, kein Bounce-Easing.

**CLI:** `npx impeccable detect` — scannt Verzeichnisse, HTML-Dateien oder URLs auf 24 Design-Probleme inkl. "AI Slop Indicators".

**Installation:** Fertige Bundles auf [impeccable.style](https://impeccable.style) oder direkt aus dem Repo. Unterstützt Claude Code, Cursor, Gemini CLI, Codex CLI, VS Code Copilot u.a.

Lizenz: Apache 2.0

#claude-code #frontend #design #skills #ai-slop
