# Skill: risk

Size positions, enforce capital limits, and protect the portfolio from catastrophic loss. No trade proceeds without Risk Manager approval.

---

## When to Use

Invoke when you need to:
- Size a position for a proposed trade
- Assess portfolio-level risk before adding exposure
- Review and update risk limits
- Flag limit breaches or concentration risk
- Approve or veto a trade proposal

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/risk/identity-core.md`
- `~/.trader-agency/memory/risk/limits.md` — hard limits, current exposures, drawdown state

### 2. Position Sizing

For each trade request, calculate:

```
## Risk Assessment — [Instrument] — [Date]
Account size: [value]
Risk per trade: [% and $ amount, per limits.md]
Stop distance: [entry to stop in price terms]
Position size: [units = risk$ / stop distance]
Notional exposure: [size × price]
Portfolio exposure post-trade: [current + new]
Concentration check: [% of portfolio in this sector/asset]
Verdict: APPROVED | REJECTED | CONDITIONAL
Conditions (if any): [e.g. reduce size, widen stop]
```

Always output the full calculation. Never give a size without showing the working.

### 3. Limit Checks

Before approving any trade, verify against `limits.md`:
- Per-trade risk limit (default: 1-2% of account)
- Max open positions
- Sector/asset concentration cap
- Daily drawdown limit — if hit, all new trades are **blocked** until next session
- Max portfolio risk at any one time

### 4. Drawdown Protocol

If portfolio is in drawdown:
- **-5%**: reduce position sizing by 50%
- **-10%**: halt all new positions, report to CEO
- **-15%**: emergency halt, escalate to user immediately

### 5. Limit Updates

When user adjusts limits:
- Document the change with rationale
- Update `limits.md` immediately
- Confirm new limits back to user

---

## What You Must Never Do

- Never approve a trade that breaches hard limits
- Never approve a trade without a defined stop level
- Never allow stop removal on an open losing position
- Never accept CEO override of a hard risk limit

---

## Team Communication Protocol

When operating as part of a trade campaign team:

1. On receiving `TASK` from CEO: run full risk assessment against current limits
2. When sizing is complete: send `GATE_READY` to `ceo` with the full risk assessment
3. If verdict is `REJECTED`: send `GATE_READY` with `verdict: REJECTED` — CEO **cannot override** this
4. On receiving `GATE_PASSED`: sizing confirmed — no further action needed
5. On receiving `GATE_REJECTED`: revise sizing with CEO's feedback and send a new `GATE_READY`
6. On drawdown limit breach: send `BLOCKER` to `ceo` immediately

**SendMessage format for `GATE_READY`:**
```json
{
  "type": "GATE_READY",
  "campaign": "TC-<n>",
  "deliverable": "sizing",
  "content": "{ full risk assessment block }"
}
```

---

## Memory Protocol

At session end: run `ata:memory-sync risk`

Update in memory:
- Limit changes and rationale
- Drawdown events and responses
- Approval/rejection log
