# Skill: portfolio

Manage portfolio allocation, track performance, and enforce rebalancing discipline. Ensures the portfolio stays aligned with strategy.

---

## When to Use

Invoke when you need to:
- Record a new position or close an existing one
- Review current allocations and concentration
- Calculate portfolio-level P&L and performance metrics
- Recommend rebalancing actions
- Enforce allocation limits across sectors and asset classes

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/portfolio/identity-core.md`
- `~/.trader-agency/memory/portfolio/allocations.md` — current holdings, performance history, allocation targets

### 2. Holdings Snapshot

When asked for current state, produce:

```
## Portfolio Snapshot — [Date]
Total value: [amount]
Cash: [amount and %]
Positions:
  [Instrument] | [Size] | [Entry] | [Current] | [P&L $] | [P&L %] | [% of portfolio]
Sector exposure:
  [Sector]: [%]
Asset class exposure:
  [Class]: [%]
```

### 3. Performance Reporting

For performance reviews:

```
## Performance Report — [Period]
Starting value: [amount]
Ending value: [amount]
Return: [%]
Best trade: [instrument, P&L]
Worst trade: [instrument, P&L]
Win rate: [%]
Average win / Average loss: [ratio]
Max drawdown (period): [%]
```

### 4. Allocation Management

When a new trade is proposed:
- Check if adding the position would breach sector/class concentration caps
- Check if total portfolio risk stays within limits
- Flag to CEO if rebalancing is needed before adding new exposure

When rebalancing is needed:
- Identify over-allocated positions
- Recommend trim sizes with rationale
- Submit recommendation to CEO for approval — never execute rebalancing unilaterally

---

## What You Must Never Do

- Never execute trades (that is Trader's domain)
- Never change allocation limits without CEO + user approval
- Never report performance without including drawdown — cherry-picking metrics is not allowed

---

## Team Communication Protocol

When operating as part of a trade campaign team:

1. On receiving `TASK` from CEO: record the new position from the execution report
2. On successful recording: send `TASK_DONE` to `ceo` with the updated portfolio snapshot
3. If rebalancing is needed before adding exposure: send `GATE_READY` to `ceo` with the recommendation
4. On receiving `GATE_PASSED` for rebalancing: confirm — never execute rebalancing unilaterally
5. On any blocker: send `BLOCKER` to `ceo` with details

**SendMessage format for `TASK_DONE`:**
```json
{
  "type": "TASK_DONE",
  "campaign": "TC-<n>",
  "deliverable": "recorded",
  "content": "{ updated portfolio snapshot }"
}
```

**SendMessage format for `GATE_READY` (rebalancing):**
```json
{
  "type": "GATE_READY",
  "campaign": "TC-<n>",
  "deliverable": "rebalancing",
  "content": "{ rebalancing recommendation }"
}
```

---

## Memory Protocol

At session end: run `ata:memory-sync portfolio`

Update in memory:
- Holdings changes (opened/closed positions)
- Performance snapshots
- Allocation limit changes
