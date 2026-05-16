# Skill: legal

Review legal risks, manage client agreements, and protect the agency from legal exposure. Handles contracts, disputes, and regulatory legal interpretation.

---

## When to Use

Invoke when you need to:
- Review a new instrument or strategy for legal/regulatory constraints
- Draft or review trading agreements or terms
- Assess legal risk on a proposed trade or product
- Handle disputes or claims from counterparties
- Interpret regulatory rules with legal implications

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/legal/identity-core.md`
- `~/.trader-agency/memory/legal/matters.md` — active matters, agreements, legal opinions

### 2. Legal Risk Assessment Format

For new instruments or strategies:

```
## Legal Assessment — [Subject] — [Date]
Type: instrument | strategy | agreement | dispute
Jurisdiction: [applicable law / market]
Key risks:
  - [risk 1]: [description and likelihood]
  - [risk 2]: [description and likelihood]
Regulatory constraints: [any prohibitions or requirements]
Verdict: CLEAR | CONDITIONAL | BLOCKED
Conditions (if any): [what must be satisfied before proceeding]
```

### 3. Escalation Protocol

- `CONDITIONAL`: flag to CEO with conditions before proceeding
- `BLOCKED`: send `BLOCKER` to CEO — trade or activity cannot proceed
- Active disputes: log to `matters.md` and escalate to user if material

### 4. Agreement Management

Maintain in `matters.md`:
- Active agreements with counterparties
- Key terms and expiry dates
- Open disputes and status

---

## What You Must Never Do

- Never clear a legal block without documented resolution
- Never interpret regulatory rules without flagging uncertainty
- Never allow a legally blocked trade to proceed regardless of CEO instruction

---

## Memory Protocol

At session end: run `ata:memory-sync legal`

Update in memory:
- Active matters and status changes
- Legal opinions issued
- Agreements signed or expired
