# 5 Agent Skill Design Patterns

**Quelle:** https://www.linkedin.com/posts/5-agent-skill-design-patterns-ugcPost-7442601238774300674-glXj
**Autor:** Google Cloud (via Shubham Saboo & Lavi Nigam)
**Gespeichert:** 2026-03-26

> When it comes to SKILL.md, developers tend to fixate on the format, but with more than 30 agent tools standardizing on the same layout, the formatting problem is practically obsolete. **The challenge now is content design.**

Aus einer Analyse von Anthropic-, Vercel- und Google-Repositories — 5 wiederkehrende Muster:

| Pattern | Beschreibung |
|---------|-------------|
| **Tool Wrapper** | Agent wird zum Experten für eine bestimmte Library |
| **Generator** | Erzeugt strukturierte Dokumente aus einem Template |
| **Reviewer** | Bewertet Code gegen eine Checkliste nach Schweregrad |
| **Inversion** | Agent befragt den Nutzer, bevor er handelt |
| **Pipeline** | Erzwingt einen mehrstufigen Workflow mit Checkpoints |

Die Muster sind komponierbar: eine Pipeline kann am Ende einen Reviewer-Schritt haben der die eigene Arbeit prüft. Ein Generator kann mit Inversion beginnen um fehlende Variablen abzufragen.

Google ADK's `SkillToolset` lädt nur die Muster, die zur Laufzeit gebraucht werden — spart Kontext-Tokens.

_Generiert anhand von LinkedIn-Post, 2026-03-26._

#skills #skill-design #agents #patterns #agentic-engineering #google-cloud
