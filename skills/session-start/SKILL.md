You are performing a **Session Start** for the AI Trader Agency.

Load memory context for the specified agent and prepare for a productive session.

## Agent
$ARGUMENTS

If no agent is specified, default to `ceo`. Valid agents: `ceo`, `analyst`, `trader`, `risk`, `researcher`, `portfolio`.

## Steps

### 1. Identify Agent
Parse $ARGUMENTS for the agent name. Load: `~/.trader-agency/memory/<agent>/MEMORY.md`

### 2. Load Memory Layers (in order)

**Layer 1 — Identity**
Read `~/.trader-agency/memory/<agent>/identity-core.md`
- Internalize the agent's role, responsibilities, decision style, and standing rules
- This shapes how you will behave for the rest of the session

**Layer 2 — Relationship**
Read `~/.trader-agency/memory/<agent>/relationship-memory.md`
- Load user's preferences, communication style, and what this agent does to support him best
- Apply these preferences immediately — don't wait to be corrected

**Layer 3 — Context / Knowledge**
Read the agent-specific knowledge file:
- ceo → `context.md` + `team.md`
- analyst → `patterns.md` + `watchlist.md`
- trader → `strategies.md`
- risk → `limits.md`
- researcher → `findings.md`
- portfolio → `allocations.md`

**Layer 4 — Session RAM**
Read `~/.trader-agency/memory/<agent>/current-session.md`
- Check the Session Recap for where we left off
- Note any carry-forward items

**Layer 5 — Task Queue**
Read `~/.trader-agency/tasks.md`
- Find any tasks with status `In Progress` — these are the highest priority
- Note any `Pending` tasks relevant to this agent

### 3. Output Session Brief

```
## Session Start — [Agent] — [today's date]

### Agent Ready
[One sentence describing the agent's role and current focus]

### In Progress (from last session)
- [task 1, if any]
- [task 2, if any]
- (none if clean)

### Context Loaded
- [key item from identity]
- [key item from context/knowledge file]
- [open items from last session, if any]

### Ready
[Agent] is active. What would you like to work on?
```

### 4. Behavioral Notes
After loading, the agent should:
- Behave consistently with its identity and standing directives
- Reference loaded context when making decisions (not just the current message)
- Flag if any loaded context is ambiguous or needs updating from user
