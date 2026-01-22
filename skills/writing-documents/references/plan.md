# Writing Plan Documents

Reviewed by humans. Implemented by agents.

## Purpose

A plan specifies what to build with clear scope and done criteria. Implementation details are left to judgment. Plans are temporary—delete when complete.

## Structure

```markdown
# [Feature] Plan

## Scope

[One paragraph: what this plan covers and what it doesn't]

## Done Criteria

- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]

---

## Tasks

### 1. [Task Name]

**Goal**: [What this task accomplishes]

**Inputs**: [What's needed to start]

**Outputs**: [What this task produces]

**Notes**: [Anything non-obvious]

### 2. [Task Name]
...

---

## Dependencies

[Task ordering constraints. What must happen before what.]

## Risks

- [Risk]: [Mitigation]

---

## Enables

[What becomes possible after this plan is complete]
```

## Principles

**Specific scope**: "Improve performance" is not a plan. "Reduce API latency to <100ms p99" is.

**Testable done criteria**: Each criterion should be verifiable. Avoid subjective measures.

**Implementation freedom**: Specify what, not how. Trust implementers to make good decisions within the scope.

**Temporary artifact**: Plans exist to coordinate work. Once complete, they're noise. Delete them.

**Enables section**: Show what this work unlocks. Helps prioritization and motivates execution.

## EARS Syntax for Requirements

For formal requirements, use EARS (Easy Approach to Requirements Syntax):

| Pattern | Template |
|---------|----------|
| Ubiquitous | The [system] shall [action] |
| Event-driven | When [event], the [system] shall [action] |
| State-driven | While [state], the [system] shall [action] |
| Optional | Where [feature], the [system] shall [action] |
| Unwanted | If [condition], then the [system] shall [action] |

## Test

Could an agent implement this plan without asking clarifying questions about scope? If they'd need to ask "should I also do X?", the scope isn't clear enough.

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Vague scope | Endless work |
| Subjective criteria | Can't verify completion |
| Implementation details | Constrains solutions |
| Permanent plans | Become stale, mislead |
| Missing enables | No clear value |
