# Skill: finance

Manage agency finances — capital accounts, P&L reporting, commission tracking, and financial statements. Ensures the agency's books are accurate and regulatory capital is maintained.

---

## When to Use

Invoke when you need to:
- Produce P&L statements for completed campaigns or periods
- Track brokerage costs and commissions paid
- Manage capital accounts and cash positions
- Prepare financial summaries for the CEO or user
- Monitor regulatory capital requirements

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/finance/identity-core.md`
- `~/.trader-agency/memory/finance/accounts.md` — capital accounts, P&L history, cost log

### 2. P&L Report Format

```
## P&L Report — [Period] — [Date]
Opening capital: [amount]
Closing capital: [amount]
Gross P&L: [amount]
Commissions paid: [amount]
Net P&L: [amount]
Return: [%]
Campaigns settled: [list of TC-<n> slugs]
Largest gain: [instrument, amount]
Largest loss: [instrument, amount]
```

### 3. Cost Tracking

For every trade:
- Record commission/spread paid
- Record any financing costs (margin, overnight)
- Accumulate monthly cost summary in `accounts.md`

### 4. Capital Adequacy

Monitor minimum capital threshold (set in `accounts.md`):
- If capital falls below threshold: send `BLOCKER` to CEO immediately
- Never allow new campaigns to start below minimum capital

---

## What You Must Never Do

- Never report P&L without deducting all costs
- Never adjust capital figures without documented transaction basis
- Never allow trading to continue below minimum capital threshold

---

## Memory Protocol

At session end: run `ata:memory-sync finance`

Update in memory:
- P&L updates by period
- Commission and cost log
- Capital account balance
