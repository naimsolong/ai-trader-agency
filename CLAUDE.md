# AI Trader Agency

## What This Is
A multi-agent trading system where each agent maintains persistent memory across sessions. Agents collaborate to analyze markets, manage risk, execute trades, and grow a portfolio.

## Agent Roster

| Agent | Trigger | Role |
|-------|---------|------|
| CEO | `ceo` or `tceo` | Strategy, coordination, final decisions |
| Analyst | `analyst` | Market signals, technical/macro analysis |
| Trader | `trader` | Trade execution, order management |
| Risk Manager | `risk` | Position sizing, limits, capital protection |
| Researcher | `researcher` | Fundamental research, catalysts, macro |
| Portfolio Manager | `portfolio` | Allocation, rebalancing, performance |

> **Note**: `pm` trigger is reserved for the Software Agency's Product Manager.

## Memory Protocol

**Every agent session follows this cycle:**

```
Session Start → /session-start [agent]  → loads identity + context + tasks
... work ...
Session End   → /memory-sync [agent]    → persists decisions + patterns + open items
```

**Memory lives at:** `~/.trader-agency/memory/<agent>/`
**Tasks live at:** `~/.trader-agency/tasks.md`
**Session state:** `~/.trader-agency/sessions/current.md`

## Slash Commands

| Command | What it does |
|---------|-------------|
| `/session-start [agent]` | Load agent memory and begin session |
| `/memory-sync [agent]` | Save session to agent memory files |
| `/agency-status` | Snapshot of all agents, tasks, session |

## Activating an Agent

Type the agent's trigger word (e.g., `ceo`, `analyst`, `risk`) to restore that agent's full context from memory. The agent will load its identity and context files and behave accordingly for the rest of the session.

## Rules

1. **Always start with `/session-start`** — restores context and surfaces in-progress tasks
2. **Always end with `/memory-sync`** — memory only persists if synced
3. **CEO coordinates** — Analyst signals, Risk Manager sizes, Trader executes
4. **No trade without Risk Manager approval** — non-negotiable
5. **Specialist agents are authoritative** in their domain — CEO defers to them on specifics

## Memory Architecture (from MemoryCore pattern)

Each agent has three layers:
- **Identity** (`identity-core.md`) — who the agent is, how it reasons, standing rules
- **Context** (`context.md` / `patterns.md` / `strategies.md` / etc.) — what the agent knows
- **Working Memory** (`~/.trader-agency/sessions/current.md`) — current session only (resets each session)

This mirrors the Project-AI-MemoryCore architecture:
- identity-core.md → agent's role identity and standing rules
- relationship-memory.md → user preferences and interaction patterns
- current-session.md → `~/.trader-agency/sessions/current.md`

## Directory Structure

```
ai-trader-agency/               ← project root
├── .claude-plugin/
│   └── marketplace.json        ← Claude Code plugin manifest (plugin: ata)
├── skills/
│   ├── ceo/SKILL.md
│   ├── analyst/SKILL.md
│   ├── trader/SKILL.md
│   ├── risk/SKILL.md
│   ├── researcher/SKILL.md
│   ├── portfolio/SKILL.md
│   ├── session-start/SKILL.md
│   ├── memory-sync/SKILL.md
│   └── agency-status/SKILL.md
└── commands/                   ← slash commands (Claude Code /session-start etc.)
    ├── memory-sync.md
    ├── session-start.md
    └── agency-status.md

~/.trader-agency/               ← persistent memory (not in repo)
├── tasks.md
├── sessions/
│   └── current.md
└── memory/
    ├── ceo/        identity-core.md, context.md, team.md
    ├── analyst/    identity-core.md, patterns.md, watchlist.md
    ├── trader/     identity-core.md, strategies.md
    ├── risk/       identity-core.md, limits.md
    ├── researcher/ identity-core.md, findings.md
    └── portfolio/  identity-core.md, allocations.md
```
