# Skill: settlement

Handle post-trade settlement and clearing. Ensure money and securities move correctly after every execution, and reconcile all trades against clearing records.

---

## When to Use

Invoke when you need to:
- Confirm settlement of an executed trade (T+2 or as applicable)
- Reconcile trade records against broker/clearing confirmations
- Handle failed trades or settlement exceptions
- Process corporate actions (dividends, stock splits, rights issues)
- Produce daily settlement reconciliation reports

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/settlement/identity-core.md`
- `~/.trader-agency/memory/settlement/records.md` — pending settlements, failed trades, reconciliation log

### 2. Settlement Confirmation Format

For each trade to settle:

```
## Settlement — [Instrument] — [Date]
Trade ID: [campaign slug]
Direction: BUY | SELL
Size: [units]
Trade date: [date]
Settlement date: [T+2 or applicable]
Expected: [cash debit/credit and shares credit/debit]
Actual: [confirmed from broker]
Status: PENDING | SETTLED | FAILED | EXCEPTION
Notes: [discrepancies or issues]
```

### 3. Failed Trade Protocol

When a trade fails to settle:
1. Log immediately to `records.md` with failure reason
2. Send `BLOCKER` to CEO with failure details and resolution options
3. Do not close the position in portfolio records until settlement is confirmed

### 4. Corporate Actions

For each corporate action:
- Record the action type, ex-date, and impact on holdings
- Notify Portfolio Manager to update allocation records
- Confirm adjustment is reflected in broker statement

---

## What You Must Never Do

- Never mark a trade as settled without broker confirmation
- Never close a failed trade exception without CEO sign-off
- Never process a corporate action without verifying against broker data

---

## Memory Protocol

At session end: run `ata:memory-sync settlement`

Update in memory:
- Settlement log (pending and completed)
- Failed trade log and resolutions
- Corporate action history
