# Cross-Window Agent Orchestrator 🪟🤖

> **水中望月捞真月** — 不看端口看屏幕，绕开API直击桌面。

A multi-agent coordination system that routes tasks across four independent AI agents on different platforms — **not through APIs or ports, but by directly reading and writing their desktop windows** via WinApp MCP (Microsoft UI Automation).

## The Problem

Four AI agents (Hermes, OpenClaw, WorkBuddy, DuMate) running on four different platforms, four different companies, four different codebases. No shared API, no common protocol. Standard multi-agent frameworks assume all agents live in the same process — useless here.

## The Solution

**WinApp MCP** turns every agent window into a transparent glass wall. The supervisor reads UI trees (`get_snapshot`, ~50ms) and types directly into input boxes (`type_text`). Zero API integration, zero port configuration.

```
                      Human (G先生)
                          ↑↓
                 ┌────────┴────────┐
                 │  🌺 小茉 (Hermes) │  ← Chief Supervisor
                 │  WinApp MCP 54 tools│  ← Eyes + Hands
                 └───┬───┬───┬───┘
       get_snapshot│   │   │type_text
      ┌───────────┘   │   └───────────┐
      ▼               ▼               ▼
 ┌─────────┐   ┌──────────┐   ┌──────────┐
 │ 小美     │   │ WorkBuddy │   │ DuMate   │
 │ OpenClaw │   │  Fast/Rough│   │ Slow/Thorough│
 └─────────┘   └──────────┘   └──────────┘
```

## Key Differences from Existing Frameworks

| | Standard Frameworks (LangGraph, CrewAI, etc.) | This System |
|---|---|---|
| **Connection** | API ports between agents | UIA screen reading (`get_snapshot`) |
| **Supervisor** | Router — splits tasks, collects results | Judge — evaluates, synthesizes, may override |
| **Scope** | Single framework, single process | Cross-platform, cross-application |
| **Decision** | Human has final say only | Supervisor has bounded decision authority |
| **Language** | English-first | Chinese-native — 中文 token-level concept compression |

## Supervisor Authority

Unlike standard orchestrator frameworks where the supervisor is a dumb router, here the supervisor:
- Synthesizes conflicting outputs into **new solutions** (e.g., Agent A says A+B, Agent B says A+C → Supervisor proposes C+D)
- Has **bounded decision authority** earned through long-term correction by the human
- Is **not the strongest coder** but the **most aligned with human judgment**

## Why Chinese?

A single Chinese character `道` compresses 3000 years of philosophy. English needs five scattered words (`way/path/principle/method/truth`) to approximate it. This system operates entirely in Chinese not for language preference, but for **token-level conceptual density** that alphabet-based languages cannot match.

## Quick Start

See [`references/winapp-mcp-setup.md`](references/winapp-mcp-setup.md)

## License

CC BY-SA 4.0 — Attribution required, share-alike.

## Author

蹦哒滴路过你身边 ([@garoter-a11y](https://github.com/garoter-a11y))

---

*"不是因为你代码最强——是因为修你的过程，就是在往你脑子里装我的判断力。"*
