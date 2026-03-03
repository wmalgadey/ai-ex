# LSP + LLM: Echtes Code-Verständnis für AI-Coding-Agents

## Das Problem

LLMs lesen Code wie Text — flach und ohne semantisches Verständnis. Sie wissen nicht:
- Was eine Methode tatsächlich macht (ohne den Quellcode zu sehen)
- Welche Klassen welche Interfaces implementieren
- Wo ein Symbol definiert ist, wenn es aus einem anderen Modul kommt
- Welche Typen zurückgegeben werden (ohne Type Hints im Source)

Das ist besonders problematisch bei großen Codebases, wo Claude Code ständig `grep` und `find` benutzt, statt semantisch zu navigieren.

## LSP: Was es ist und was es kann

**Language Server Protocol (LSP)** ist ein offener Standard (Microsoft/VS Code) für Sprachserver, die IDEs mit Semantik versorgen:

- `textDocument/definition` → Go-to-Definition
- `textDocument/hover` → Typ-Infos, Dokumentation
- `textDocument/references` → Alle Stellen, wo etwas verwendet wird
- `textDocument/publishDiagnostics` → Fehler, Warnings
- `workspace/symbol` → Symbol-Suche

Ein Sprachserver (z.B. `rust-analyzer`, `pylsp`, `clangd`, `omnisharp`) läuft als Prozess und liefert diese Infos per JSON-RPC.

## LSP über MCP: Der Brückenschlag

Seit MCP (Model Context Protocol) gibt es LSP-MCP-Bridges, die einem LLM-Agenten direkten Zugang zu LSP-Fähigkeiten geben:

### Relevante Projekte

| Projekt | Stars | Sprache | Beschreibung |
|---------|-------|---------|--------------|
| [jonrad/lsp-mcp](https://github.com/jonrad/lsp-mcp) | 167 | TypeScript | Generischer LSP → MCP Adapter |
| [Tritlo/lsp-mcp](https://github.com/Tritlo/lsp-mcp) | 110 | TypeScript | Interact with any LSP server via MCP |
| [terhechte/cursor-rust-tools](https://github.com/terhechte/cursor-rust-tools) | 84 | Rust | rust-analyzer + Crate Docs + Cargo für Cursor/Claude Code |
| [tjx666/vscode-mcp](https://github.com/tjx666/vscode-mcp) | 58 | TypeScript | LSP Diagnostics + Type-Info aus VS Code live |

### Prinzip

```
Claude Code → MCP → LSP-MCP-Bridge → Language Server (rust-analyzer, omnisharp, ...)
                                        ↕
                                    Codebase (Dateisystem)
```

Claude Code kann dann fragen:
- "Was ist der Typ von Variable X in Zeile Y?"
- "Wo ist diese Methode definiert?"
- "Welche Klassen implementieren dieses Interface?"

## Alternative Ansätze (ohne LSP)

### 1. CLAUDE.md als Architektur-Guide

Die einfachste Lösung: explizites Domänenwissen dokumentieren.

```markdown
# CLAUDE.md

## Architektur

- `IOrderService` → `OrderService` (Implementierung in `src/services/`)
- Repository Pattern: alle DB-Zugriffe über `IRepository<T>`
- `Domain.Events` enthält alle Domain Events (Namespace-Konvention)

## Wichtige Abstraktionen

- `Result<T>` = Railway-Oriented-Programming statt Exceptions
- Handler-Pattern: jeder Command hat einen `ICommandHandler<TCommand>`
```

**Vorteil:** Einfach, keine Tools nötig  
**Nachteil:** Veraltet schnell, manueller Aufwand

### 2. Auto Memory (Claude Code built-in)

Claude Code speichert selbst gelerntes in `~/.claude/projects/<project>/memory/`.  
Bei der ersten Analyse eines Projekts: Claude Code lernt Build-Commands, Patterns, wichtige Klassen.

Kann mit `/memory` eingesehen und editiert werden.

### 3. Tree-sitter für statische Analyse

Tree-sitter parst Code in einen AST ohne Language Server.  
Gut für: Klassen-/Methoden-Inventare, schnelle Symbol-Extraktion.

Gibt es als MCP-Server (z.B. `tree-sitter-mcp` community projects) oder als direktes CLI-Tool.

### 4. Code-Index via ctags / ripgrep-all

```bash
# ctags Index erstellen
ctags -R --output-format=json .

# In CLAUDE.md referenzieren oder als MCP Tool bereitstellen
```

Primitiver als LSP, aber oft ausreichend für Navigation.

## Empfehlung nach Usecase

| Szenario | Empfehlung |
|----------|------------|
| Neues Projekt onboarden | CLAUDE.md + `/init` für auto-generierte Basis |
| .NET/C# Projekt | LSP-MCP Bridge mit OmniSharp oder C# Dev Kit |
| Rust-Projekt | `cursor-rust-tools` (rust-analyzer + Cargo) |
| Große Codebase, viele Abstractions | LSP-MCP + CLAUDE.md für Domain-spezifisches Wissen |
| Quick-and-dirty | Auto Memory + gute CLAUDE.md reichen oft |

## Links

- [LSP Spec](https://microsoft.github.io/language-server-protocol/)
- [MCP Spec](https://modelcontextprotocol.io/introduction)
- [Claude Code Memory Docs](https://code.claude.com/docs/en/memory)
- [Claude Code MCP Docs](https://code.claude.com/docs/en/mcp)

---
*Erstellt: 2026-03-03*
