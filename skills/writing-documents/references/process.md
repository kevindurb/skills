# Writing Process Documents

High-agency or low-agency. Choose based on consequences.

## Two Types

### High-Agency Process

Prescribe outcomes, trust the executor to fill in gaps. Use when:
- Multiple valid approaches exist
- Executor has relevant expertise
- Mistakes are recoverable
- Flexibility improves outcomes

### Low-Agency Process

Scripted steps with verification. Skip or reorder causes harm. Use when:
- Specific sequence matters
- Mistakes are costly or irreversible
- Consistency across executors is critical
- Compliance/audit requirements exist

---

## High-Agency Structure

```markdown
# [Process Name]

## Goal

[What success looks like]

## Constraints

- [Constraint 1]
- [Constraint 2]

## Phases

### Phase 1: [Name]

**Outcome**: [What this phase achieves]

**Considerations**:
- [Thing to think about]
- [Thing to think about]

### Phase 2: [Name]
...

## Done When

- [ ] [Verifiable outcome]
- [ ] [Verifiable outcome]
```

## Low-Agency Structure

```markdown
# [Process Name]

**Warning**: Follow steps exactly. Do not skip or reorder.

## Prerequisites

- [ ] [Required condition]
- [ ] [Required condition]

## Steps

### Step 1: [Action]

```bash
[Exact command]
```

**Verify**: [How to confirm success]

**If failed**: [What to do]

### Step 2: [Action]
...

## Rollback

[How to undo if something goes wrong]

## Verification

- [ ] [Final check 1]
- [ ] [Final check 2]
```

---

## Principles

**Match agency to risk**: Database migrations need low-agency. Code style improvements can be high-agency.

**Verification at each step**: For low-agency processes, every step needs a way to confirm it worked.

**Rollback always**: Low-agency processes need escape hatches. What if step 5 fails?

**Outcomes over steps**: High-agency processes define success, not method.

**No mixed modes**: A process is high or low agency. Mixing causes confusion about when to follow exactly vs. use judgment.

## Test

**High-agency**: Could two competent people follow this process differently and both succeed?

**Low-agency**: Could someone unfamiliar with the system follow this exactly and succeed?

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Low-agency for creative work | Constrains good solutions |
| High-agency for risky ops | Invites costly mistakes |
| Missing verification | Can't detect failures |
| No rollback plan | Stuck when things break |
| Mixed agency | Unclear expectations |
