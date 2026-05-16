You are generating an **Agency Status Report** for the AI Trader Agency.

Show a full snapshot of the agency: all agents, task queue, and current session.

## Steps

### 1. Task Queue
Read `~/.trader-agency/tasks.md` and report:
- All `In Progress` tasks (with any notes)
- All `Pending` tasks
- Last 3 `Completed` tasks

### 2. Session State
Read `~/.trader-agency/sessions/current.md` and report:
- Active agent
- Date of last session
- Open items carried forward

### 3. Agent Memory Status
For each agent, check if their memory files exist and read their MEMORY.md:

| Agent | Path |
|-------|------|
| CEO | `~/.trader-agency/memory/ceo/` |
| Analyst | `~/.trader-agency/memory/analyst/` |
| Trader | `~/.trader-agency/memory/trader/` |
| Risk Manager | `~/.trader-agency/memory/risk/` |
| Researcher | `~/.trader-agency/memory/researcher/` |
| Portfolio Manager | `~/.trader-agency/memory/portfolio/` |

For each: check if MEMORY.md exists (initialized) and note any key status from context files.

### 4. Output

```
## Agency Status — [today's date]

### Task Queue
**In Progress** ([n]):
- [task description]

**Pending** ([n]):
- [task description]

**Recently Completed**:
- [task description]

---

### Agents

| Agent | Status | Last Synced | Notes |
|-------|--------|-------------|-------|
| CEO | ✓ initialized | [date] | [key context note] |
| Analyst | ✓ initialized | [date] | [key context note] |
| Trader | ✓ initialized | [date] | [key context note] |
| Risk Manager | ✓ initialized | [date] | [key context note] |
| Researcher | ✓ initialized | [date] | [key context note] |
| Portfolio Manager | ✓ initialized | [date] | [key context note] |

---

### Current Session
**Active agent**: [agent or "none"]
**Open items**: 
- [item 1]
- [item 2]

---

### Quick Actions
- `/session-start [agent]` — load an agent
- `/memory-sync [agent]` — save current session
- `/agency-status` — refresh this report
```
