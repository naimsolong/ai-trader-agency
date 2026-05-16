You are performing a **Memory Sync** for the AI Trader Agency.

Persist the current session's important information to the appropriate agent's memory files.

## Agent
$ARGUMENTS

If no agent is specified, default to `ceo`. Valid agents: `ceo`, `analyst`, `trader`, `risk`, `researcher`, `portfolio`.

## Steps

### 1. Identify the Active Agent
Determine which agent's memory to update based on $ARGUMENTS or the conversation context.
- Agent memory path: `~/.trader-agency/memory/<agent>/`

### 2. Extract Session Intelligence
Scan the conversation and extract:

**Decisions Made**
- What was decided and why (include rationale — this is what makes memory useful)
- Format: `### [today's date] — [Decision Title]` / `**Decision**: ...` / `**Rationale**: ...` / `**Status**: active`

**Patterns Discovered**
- Any market patterns, user behavior patterns, or agent performance observations
- Format: `### [Pattern Name]` / `**Observed**: ...` / `**Confidence**: low|medium|high` / `**First seen**: [date]`

**User Preference Signals**
- Any corrections, approvals, preferences user expressed
- Add to the agent's context file under "User Preference Signals"

**Open Items**
- Unresolved tasks, pending decisions, blockers
- These go to `~/.trader-agency/sessions/current.md` under "Open Items"

**Task Queue Changes**
- Any tasks that changed state (started, completed, new tasks created)
- Update `~/.trader-agency/tasks.md` accordingly

### 3. Write Updates
Update only the sections that changed. Do not overwrite sections with no changes.

For each agent, the files are:
- `ceo`: context.md (decisions, user signals), team.md (coordination notes)
- `analyst`: patterns.md (new patterns), watchlist.md (new instruments/view changes)
- `trader`: strategies.md (execution log, strategy updates)
- `risk`: limits.md (limit changes, drawdown events)
- `researcher`: findings.md (new research, macro updates)
- `portfolio`: allocations.md (holdings changes, performance snapshot)

Also update:
- `~/.trader-agency/memory/<agent>/current-session.md` — update Session Recap and clear Working Memory for next session
- `~/.trader-agency/tasks.md` — update task states

### 4. Confirm Sync

After writing, output a brief confirmation:

```
## Memory Sync Complete — [agent] — [date]

### Files Updated
- [list files that were changed]

### Persisted
- [bullet list of what was saved]

### Carried Forward
- [open items for next session]
```
