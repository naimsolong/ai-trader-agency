# AI Trader Agency

## What This Is
A multi-agent trading system where each agent maintains persistent memory across sessions. Agents collaborate to analyze markets, manage risk, execute trades, and grow a portfolio.

## Agent Roster

### Front Office
| Agent | Trigger | Role |
|-------|---------|------|
| CEO | `ceo` | Strategy, coordination, final decisions |
| Technical Analyst | `technical-analyst` | Price action, chart patterns, trade signals |
| Fundamental Analyst | `fundamental-analyst` | Company research, macro catalysts, theses |
| Dealer | `dealer` | Trade execution, order management |
| Portfolio Manager | `portfolio` | Allocation, rebalancing, performance |

### Middle Office
| Agent | Trigger | Role |
|-------|---------|------|
| Risk Manager | `risk` | Position sizing, limits, capital protection |
| Compliance Officer | `compliance` | Regulatory adherence, trade review, AML/KYC |
| Internal Audit | `audit` | Process audits, control reviews, findings |
| Product Development | `product-development` | Strategy design, workflow improvements, roadmap |

### Back Office
| Agent | Trigger | Role |
|-------|---------|------|
| Settlement | `settlement` | Post-trade clearing, reconciliation, corporate actions |
| Custody | `custody` | Holdings safekeeping, position records, income tracking |
| Finance | `finance` | P&L reporting, cost tracking, capital accounts |
| Legal | `legal` | Legal risk, agreements, regulatory interpretation |

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

Type the agent's trigger word (e.g., `ceo`, `technical-analyst`, `risk`) to restore that agent's full context from memory. The agent will load its identity and context files and behave accordingly for the rest of the session.

## Rules

1. **Always start with `/session-start`** — restores context and surfaces in-progress tasks
2. **Always end with `/memory-sync`** — memory only persists if synced
3. **CEO coordinates** — Technical Analyst signals, Risk Manager sizes, Dealer executes
4. **No trade without Risk Manager approval** — non-negotiable
5. **No trade without Compliance clearance** — non-negotiable
6. **Specialist agents are authoritative** in their domain — CEO defers to them on specifics

## Memory Architecture (from MemoryCore pattern)

Each agent has three layers:
- **Identity** (`identity-core.md`) — who the agent is, how it reasons, standing rules
- **Context** (`context.md` / `patterns.md` / `strategies.md` / etc.) — what the agent knows
- **Working Memory** (`~/.trader-agency/sessions/current.md`) — current session only (resets each session)

## Directory Structure

```
ai-trader-agency/               ← project root
├── .claude-plugin/
│   └── marketplace.json        ← Claude Code plugin manifest (plugin: ata)
├── skills/
│   ├── ceo/SKILL.md
│   ├── technical-analyst/SKILL.md
│   ├── fundamental-analyst/SKILL.md
│   ├── dealer/SKILL.md
│   ├── portfolio/SKILL.md
│   ├── risk/SKILL.md
│   ├── compliance/SKILL.md
│   ├── audit/SKILL.md
│   ├── product-development/SKILL.md
│   ├── settlement/SKILL.md
│   ├── custody/SKILL.md
│   ├── finance/SKILL.md
│   ├── legal/SKILL.md
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
    ├── ceo/                    identity-core.md, context.md, team.md
    ├── technical-analyst/      identity-core.md, patterns.md, watchlist.md
    ├── fundamental-analyst/    identity-core.md, findings.md
    ├── dealer/                 identity-core.md, strategies.md
    ├── portfolio/              identity-core.md, allocations.md
    ├── risk/                   identity-core.md, limits.md
    ├── compliance/             identity-core.md, rules.md
    ├── audit/                  identity-core.md, reports.md
    ├── product-development/    identity-core.md, roadmap.md
    ├── settlement/             identity-core.md, records.md
    ├── custody/                identity-core.md, holdings.md
    ├── finance/                identity-core.md, accounts.md
    └── legal/                  identity-core.md, matters.md
```
