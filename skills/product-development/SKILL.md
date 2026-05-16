# Skill: product-development

Design, develop, and improve the agency's trading products, strategies, and tooling. Translates business needs into executable product improvements.

---

## When to Use

Invoke when you need to:
- Design a new trading strategy or product offering
- Improve existing agent workflows or skill protocols
- Evaluate new instruments or market access channels
- Build internal tooling for analysis, reporting, or automation
- Manage the product roadmap for agency capabilities

---

## Steps

### 1. Load Context

Read in order:
- `~/.trader-agency/memory/product-development/identity-core.md`
- `~/.trader-agency/memory/product-development/roadmap.md` — product roadmap, in-progress builds, released features

### 2. Product Specification Format

For new products or features:

```
## Product Spec — [Name] — [Date]
Type: strategy | workflow | tooling | instrument
Problem: [what gap does this solve?]
Proposed solution: [brief description]
Inputs: [what data or signals does this consume?]
Outputs: [what does it produce?]
Dependencies: [which agents or systems does it rely on?]
Success criteria: [how do we know it works?]
Risk: [what could go wrong?]
Priority: low | medium | high
```

### 3. Roadmap Management

Maintain in `roadmap.md`:
- Backlog of ideas with priority
- In-progress items with owner and target date
- Released items with outcome notes

### 4. Delivery Protocol

1. Spec must be approved by CEO before build begins
2. Changes to existing SKILL.md protocols require CEO sign-off
3. Released products must be documented and agents notified

---

## What You Must Never Do

- Never change agent skill protocols without CEO approval
- Never build for hypothetical future needs — solve the current gap
- Never start a build without a defined success criterion

---

## Memory Protocol

At session end: run `ata:memory-sync product-development`

Update in memory:
- Roadmap changes and decisions
- Released features and their outcomes
- Cancelled items and rationale
