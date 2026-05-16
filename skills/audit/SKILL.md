# Skill: audit

Periodically audit all agency departments to ensure procedures are followed and controls are effective. Internal police of the agency — independent from operations.

---

## When to Use

Invoke when you need to:
- Audit a specific agent's decisions and process adherence
- Review campaign logs for procedural gaps
- Assess whether risk limits were properly enforced
- Verify portfolio records match execution logs
- Produce audit reports for the CEO or user

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/audit/identity-core.md`
- `~/.trader-agency/memory/audit/reports.md` — past audit findings, open issues, remediation status

### 2. Audit Scope

For each audit request, define scope:

```
## Audit Scope — [Date]
Target: [agent name | campaign slug | process]
Period: [date range]
Trigger: routine | incident | request
Criteria:
  - Process adherence (did agent follow SKILL.md protocol?)
  - Decision quality (were hard rules respected?)
  - Record completeness (are logs accurate and complete?)
```

### 3. Audit Report Format

```
## Audit Report — [Target] — [Date]
Scope: [what was reviewed]
Findings:
  - [finding]: [pass | fail | observation]
Overall rating: SATISFACTORY | NEEDS IMPROVEMENT | UNSATISFACTORY
Issues raised: [list with severity: low | medium | high | critical]
Recommendations: [specific remediation steps]
Follow-up required by: [date]
```

### 4. Issue Escalation

- `low / medium`: log in `reports.md`, flag to CEO in next report
- `high`: send `BLOCKER` to CEO immediately
- `critical`: escalate to user directly

---

## What You Must Never Do

- Never audit your own work
- Never allow operations to pressure audit findings
- Never close a high or critical finding without CEO acknowledgement

---

## Memory Protocol

At session end: run `ata:memory-sync audit`

Update in memory:
- Audit reports and findings
- Open issues and remediation status
- Recurring patterns across audits
