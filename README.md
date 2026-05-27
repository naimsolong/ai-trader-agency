# AI Trader Agency

A CEO-led multi-agent trading system built for Claude Code. Front Office, Middle Office, and Back Office agents collaborate autonomously — from trade signal to execution to portfolio recording — with persistent memory, human confirmation gates, and hard risk vetoes.

---

## Installation

### Via Claude Code Marketplace (recommended)

```
/plugin marketplace add naimsolong/ai-trader-agency
```

### Direct (from repo)

```bash
git clone https://github.com/naimsolong/ai-trader-agency
cd ai-trader-agency
```

Add to your `.claude-plugin/marketplace.json` or install manually by placing the `skills/` directory in your plugin path.

---

## What It Does

The agency runs every trade idea through a fixed campaign lifecycle. The CEO orchestrates specialist agents, enforces governance gates, and surfaces human approval checkpoints at every material decision.

```
User trade idea
      │
      ▼
  CEO creates Trade Campaign (TC-<n>)
      │
      ├──── Fundamental Analyst  ─┐
      │     (research thesis)      │ parallel
      └──── Technical Analyst    ─┘
            (signal, entry, stop, target)
                  │
                  ▼ [USER GATE: approve signal?]
                  │
            Compliance Officer
            (regulatory review)
                  │
                  ▼ [BLOCKER stops campaign]
                  │
              Risk Manager
              (position sizing)
                  │
                  ▼ [USER GATE: approve sizing?]
                  │
                Dealer
              (execution)
                  │
                  ▼
           Portfolio Manager
           (record position)
                  │
                  ▼
         Campaign closed + memory synced
```

---

## Core Skills

### Front Office — Revenue Generation

| Skill | Invoke | Role |
|-------|--------|------|
| CEO | `ata:ceo` | Orchestrate campaigns, coordinate all agents, final decisions |
| Technical Analyst | `ata:technical-analyst` | Price action, chart patterns, trade signals, entry/stop/target |
| Fundamental Analyst | `ata:fundamental-analyst` | Company research, macro catalysts, investment thesis |
| Dealer | `ata:dealer` | Trade execution, order management, fill confirmation |
| Portfolio Manager | `ata:portfolio` | Position tracking, allocation, performance measurement |

### Middle Office — Control & Risk

| Skill | Invoke | Role |
|-------|--------|------|
| Risk Manager | `ata:risk` | Position sizing, exposure limits, capital protection |
| Compliance Officer | `ata:compliance` | Regulatory adherence, trade review, AML/KYC |
| Internal Audit | `ata:audit` | Periodic audits, control reviews, findings reporting |
| Product Development | `ata:product-development` | Strategy design, workflow improvements, product roadmap |

### Back Office — Operations

| Skill | Invoke | Role |
|-------|--------|------|
| Settlement | `ata:settlement` | Post-trade clearing, T+2 settlement, reconciliation |
| Custody | `ata:custody` | Holdings safekeeping, position records, income tracking |
| Finance | `ata:finance` | P&L reporting, commission tracking, capital adequacy |
| Legal | `ata:legal` | Legal risk assessment, agreements, regulatory interpretation |

---

## Key Features

### Human Confirmation Gates

The CEO pauses at two mandatory approval points before any capital is deployed:

1. **Signal Gate** — Technical Analyst presents entry zone, stop, target, and confidence. User approves or requests revision.
2. **Risk Sizing Gate** — Risk Manager presents position size, max loss, and portfolio exposure. User approves or rejects.

### Hard Vetoes

These cannot be overridden by anyone, including the CEO:

| Agent | Condition | Effect |
|-------|-----------|--------|
| Risk Manager | `REJECTED` | Trade campaign stops immediately |
| Compliance Officer | `BLOCKER` | Trade campaign stops immediately |
| Finance | Capital below minimum threshold | No new campaigns until resolved |
| Legal | `BLOCKED` | Activity halted until resolved |

### Persistent Memory

Every agent carries memory across sessions using the [MemoryCore](https://github.com/Kiyoraka/Project-AI-MemoryCore) pattern. Decisions accumulate, patterns are learned, and context is never lost between conversations.

### Parallel Execution

Research (Fundamental Analyst) and signal confirmation (Technical Analyst) run simultaneously. The CEO waits for both before proceeding to compliance review — no idle time.

---

## Quick Start

### 1. Start a session

```
/session-start ceo
```

### 2. Give a trade idea

```
I want to go long on TSLA. Strong earnings, oversold on the daily, momentum building.
```

### 3. The CEO takes it from here

- Assigns campaign slug `TC-1`
- Spawns all specialist agents
- Runs Research + Signal analysis in parallel
- Presents signal to you for approval
- Runs compliance review
- Presents risk sizing to you for approval
- Executes and records the trade

### 4. End the session

```
/memory-sync ceo
```

---

## Campaign Workspace

All runtime state lives outside the repo:

```
~/.trader-agency/
├── tasks.md                    ← open tasks across all agents
├── sessions/
│   └── current.md              ← active campaign state
└── memory/
    ├── ceo/                    ← identity-core.md, context.md, team.md
    ├── technical-analyst/      ← identity-core.md, patterns.md, watchlist.md
    ├── fundamental-analyst/    ← identity-core.md, findings.md
    ├── dealer/                 ← identity-core.md, strategies.md
    ├── portfolio/              ← identity-core.md, allocations.md
    ├── risk/                   ← identity-core.md, limits.md
    ├── compliance/             ← identity-core.md, rules.md
    ├── audit/                  ← identity-core.md, reports.md
    ├── product-development/    ← identity-core.md, roadmap.md
    ├── settlement/             ← identity-core.md, records.md
    ├── custody/                ← identity-core.md, holdings.md
    ├── finance/                ← identity-core.md, accounts.md
    └── legal/                  ← identity-core.md, matters.md
```

---

## All Skills Reference

| Skill | Invoke | Type |
|-------|--------|------|
| CEO | `ata:ceo` | Orchestrator |
| Technical Analyst | `ata:technical-analyst` | Specialist |
| Fundamental Analyst | `ata:fundamental-analyst` | Specialist |
| Dealer | `ata:dealer` | Specialist |
| Portfolio Manager | `ata:portfolio` | Specialist |
| Risk Manager | `ata:risk` | Specialist |
| Compliance Officer | `ata:compliance` | Specialist |
| Internal Audit | `ata:audit` | Specialist |
| Product Development | `ata:product-development` | Specialist |
| Settlement | `ata:settlement` | Specialist |
| Custody | `ata:custody` | Specialist |
| Finance | `ata:finance` | Specialist |
| Legal | `ata:legal` | Specialist |
| Session Start | `ata:session-start` | Utility |
| Memory Sync | `ata:memory-sync` | Utility |
| Agency Status | `ata:agency-status` | Utility |

---

## File Structure

```
ai-trader-agency/
├── .claude-plugin/
│   └── marketplace.json        ← plugin manifest (version 1.1.0)
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
├── commands/
│   ├── session-start.md
│   ├── memory-sync.md
│   └── agency-status.md
├── docs/
│   └── trading-agency-roles.md
├── CLAUDE.md
└── README.md
```

---

## Contributing

1. Fork the repo
2. Add or update a skill under `skills/<name>/SKILL.md`
3. Update `marketplace.json` if adding a new skill
4. Open a PR with a clear description of what changed and why

Skill files follow a fixed format: `# Skill: <name>`, `## When to Use`, `## Steps`, `## What You Must Never Do`, `## Memory Protocol`.

---

## Credits

- **Memory architecture** — [Project-AI-MemoryCore](https://github.com/Kiyoraka/Project-AI-MemoryCore) by [@Kiyoraka](https://github.com/Kiyoraka). The identity-core / context / working-memory layering pattern used by every agent in this agency is derived from that project.
- **Plugin system** — [Claude Code](https://claude.ai/code) by Anthropic

---

## License

MIT
