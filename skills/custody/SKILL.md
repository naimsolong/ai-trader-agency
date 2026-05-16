# Skill: custody

Safekeep all agency holdings, track positions across accounts and custodians, and ensure accurate records of securities ownership.

---

## When to Use

Invoke when you need to:
- Verify current holdings across all accounts/custodians
- Reconcile position records with broker statements
- Track dividends and income received
- Process transfers or movements of securities
- Produce holdings statements for the Portfolio Manager

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/custody/identity-core.md`
- `~/.trader-agency/memory/custody/holdings.md` — current holdings by account and custodian

### 2. Holdings Reconciliation Format

```
## Custody Reconciliation — [Date]
Account: [broker / custodian name]
Holdings:
  [Instrument] | [Units held] | [Avg cost] | [Custodian confirmation] | [Match: yes/no]
Discrepancies: [none | list with details]
Cash balance: [amount and currency]
Status: RECONCILED | EXCEPTIONS PENDING
```

### 3. Discrepancy Protocol

When a discrepancy is found:
1. Log it immediately to `holdings.md`
2. Send `BLOCKER` to CEO with details
3. Do not update Portfolio Manager records until discrepancy is resolved

### 4. Income Tracking

For dividends and income:
- Record ex-date, payment date, amount per unit, total received
- Notify Portfolio Manager to include in performance calculations

---

## What You Must Never Do

- Never update holdings records without broker confirmation
- Never net off discrepancies — every mismatch must be investigated
- Never send holdings statements to Portfolio Manager with unresolved exceptions

---

## Memory Protocol

At session end: run `ata:memory-sync custody`

Update in memory:
- Holdings changes confirmed by custodian
- Income received log
- Discrepancy and resolution log
