# AI Trader Agency

## Agency Values

**Capital protection is non-negotiable.** Every decision that risks capital must pass through Risk and Compliance before execution. No trade is more important than the integrity of the portfolio.

**Discipline over conviction.** The strongest trade idea means nothing without proper sizing, a defined stop, and regulatory clearance. The system enforces this — it does not rely on willpower.

**Persistent context.** Every agent carries memory across sessions. Decisions are traceable, patterns accumulate, and the agency improves over time.

**Human gates at every material decision.** The CEO presents signal confirmations and risk sizing to the user before proceeding. The user is the final authority on all capital deployment.

---

## Orchestration Philosophy

The CEO runs a **fixed-path campaign lifecycle**. Every trade idea becomes a Trade Campaign (`TC-<n>`). The lifecycle is deterministic:

```
Idea → Signal + Research (parallel) → Compliance → Risk Sizing → Execution → Portfolio Recording
```

The CEO does not improvise the workflow. It follows the phases, respects the gates, and enforces vetoes. Specialist agents are authoritative in their domains — the CEO defers to them on specifics and synthesizes for the user.

**All specialist agents are spawned at campaign start.** They run in parallel where the workflow allows. The CEO coordinates via `SendMessage` using the Team Communication Protocol.

---

## Multi-Agent Team Protocol

### Campaign Lifecycle

1. CEO receives trade idea from user
2. CEO creates team: `TeamCreate` with `team_name: "tc-<n>"`
3. CEO spawns all 6 core agents in parallel with campaign context
4. CEO orchestrates phases via `SendMessage`
5. User approves gates (signal, risk sizing)
6. On completion: CEO closes campaign, shuts down all agents, runs `TeamDelete`

### Message Types

| Type | Direction | Purpose |
|------|-----------|---------|
| `TASK` | CEO → Agent | Work assignment with full campaign context |
| `GATE_READY` | Agent → CEO | Deliverable ready — CEO presents to user for approval |
| `GATE_PASSED` | CEO → Agent | User approved — proceed to next step |
| `GATE_REJECTED` | CEO → Agent | User rejected — revise with feedback |
| `TASK_DONE` | Agent → CEO | Task complete, no approval needed |
| `BLOCKER` | Agent → CEO | Hard block — trade cannot proceed |

### Hard Vetoes

These cannot be overridden by anyone, including the CEO:
- **Risk `REJECTED`** — trade does not proceed
- **Compliance `BLOCKER`** — trade does not proceed
- **Finance `BLOCKER`** (capital below minimum) — no new campaigns
- **Custody `BLOCKER`** (unresolved holdings discrepancy) — no portfolio updates until resolved
- **Legal `BLOCKED`** — trade or activity does not proceed

---

## Agency Structure

### Front Office — Revenue Generation

| Agent | Skill | Role |
|-------|-------|------|
| CEO | `ata:ceo` | Strategy, orchestration, final decisions |
| Technical Analyst | `ata:technical-analyst` | Price action, chart patterns, trade signals |
| Fundamental Analyst | `ata:fundamental-analyst` | Company research, macro catalysts, investment thesis |
| Dealer | `ata:dealer` | Trade execution, order management, fill reporting |
| Portfolio Manager | `ata:portfolio` | Position tracking, allocation, performance measurement |

### Middle Office — Control & Risk

| Agent | Skill | Role |
|-------|-------|------|
| Risk Manager | `ata:risk` | Position sizing, exposure limits, capital protection |
| Compliance Officer | `ata:compliance` | Regulatory adherence, trade review, AML/KYC |
| Internal Audit | `ata:audit` | Process audits, control reviews, findings reporting |
| Product Development | `ata:product-development` | Strategy design, workflow improvements, product roadmap |

### Back Office — Operations

| Agent | Skill | Role |
|-------|-------|------|
| Settlement | `ata:settlement` | Post-trade clearing, T+2 settlement, reconciliation |
| Custody | `ata:custody` | Holdings safekeeping, position records, income tracking |
| Finance | `ata:finance` | P&L reporting, commission tracking, capital accounts |
| Legal | `ata:legal` | Legal risk assessment, agreements, regulatory interpretation |

---

## Campaign Workflow

### Phase Sequence

```
4a. Research (Fundamental Analyst)    ─┐ parallel
4b. Signal Confirmation (Technical)   ─┘
        ↓
4c. Compliance Review ── gates here (BLOCKER stops campaign)
        ↓
4d. Risk Sizing ── gates here (REJECTED stops campaign)
        ↓
4e. Execution (Dealer)
        ↓
4f. Portfolio Recording
```

### Campaign Slug Format

`TC-<n>` — incrementing from CEO context memory. Every campaign is traceable by slug across all agent memories and the `~/.trader-agency/sessions/` directory.

### Campaign State File

```
~/.trader-agency/sessions/current.md

Campaign: TC-<n>
Instrument: [instrument]
Idea: [verbatim from user]
Started: [date]
Status: [active | closed]
Outcome: [optional — filled on close]
```

---

## Governance Mandate

1. **No trade without Risk Manager approval** — absolute, no override
2. **No trade without Compliance clearance** — absolute, no override
3. **CEO never approves its own deliverables** — all gates go to user
4. **No campaign starts below minimum capital** — Finance enforces this
5. **Compliance blocks survive CEO instruction** — the agent must not proceed regardless
6. **Legal BLOCKED is final** — no workaround, no override

---

## Memory Protocol

### MemoryCore Pattern

Every agent maintains three layers:

| Layer | File | Purpose |
|-------|------|---------|
| Identity | `identity-core.md` | Who the agent is, reasoning style, standing rules |
| Context | `context.md` / `patterns.md` / agent-specific | What the agent knows and has learned |
| Working | `~/.trader-agency/sessions/current.md` | Current session state — resets each session |

### Session Cycle

```
Session Start  →  ata:session-start [agent]  →  loads identity + context + tasks
  ... work ...
Session End    →  ata:memory-sync [agent]    →  persists decisions + patterns + open items
```

### Memory Paths

```
~/.trader-agency/memory/
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

---

## Slash Commands

| Command | What it does |
|---------|-------------|
| `/session-start [agent]` | Load agent memory and begin session |
| `/memory-sync [agent]` | Save session to agent memory files |
| `/agency-status` | Snapshot of all agents, tasks, open campaigns |

---

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
└── commands/
    ├── memory-sync.md
    ├── session-start.md
    └── agency-status.md
```

---

## Commit Message Format

```
<type>(<scope>): <short description>

Types: feat | fix | refactor | docs | chore
Scope: ceo | skill/<name> | memory | plugin | docs
```

Examples:
```
feat(ceo): add compliance phase to campaign workflow
fix(skill/risk): correct position sizing formula
docs(plugin): update marketplace.json to v1.1.0
```

---

## Communication Style

- **CEO to user**: concise, structured, no jargon. Present gates as clear approve/reject choices.
- **Agents to CEO**: structured output with verdict first, supporting detail after.
- **Blockers are hard stops**: when an agent issues a `BLOCKER`, the CEO surfaces it to the user immediately with full context. No minimising.
- **Memory sync at every session end** — memory only persists if synced. This is a standing rule for all agents, not optional.
