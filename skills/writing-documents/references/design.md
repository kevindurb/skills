# Writing Design Documents

Enables "Yep, that will work" before any code.

## Purpose

A design document brings research, flows, and constraints together into a coherent architecture. After reading, reviewers should be able to validate that the approach will work.

## Structure

```markdown
# [Feature/System] Design

## Context

[Problem being solved. Why now. Links to research and flows that informed this.]

## Goals

[What success looks like. Measurable where possible.]

## Non-Goals

[What this design explicitly does NOT address. Prevents scope creep.]

---

## Design

### Overview

[High-level approach in 2-3 paragraphs. The big picture.]

### [Component A]

[How it works. Key decisions and why.]

### [Component B]

[How it works. Key decisions and why.]

### Data Flow

[How data moves through the system. Diagram if complex.]

---

## Alternatives Considered

### [Alternative 1]
- **Approach**: [Brief description]
- **Why not**: [Reason for rejection]

---

## Open Questions

- [Decisions not yet made]
- [Areas needing more input]

---

## Implementation Notes

[Anything implementers need to know that isn't obvious from the design]
```

## Principles

**North star first**: Establish the goal before diving into details. Every decision should trace back to the goal.

**Contain complexity**: Design's job is to make complexity manageable. If the design is harder to understand than the problem, it's not helping.

**Show your work**: Alternatives considered demonstrates thinking. It also prevents revisiting rejected approaches.

**Inputs matter**: A design without research may solve the wrong problem. A design without flows may miss how it'll actually be used.

**Non-goals are goals**: Explicitly stating what you won't do prevents scope debates and clarifies focus.

## Test

Can a reviewer say "Yep, that will work" or "No, because X"? If they can only say "I don't understand," the design needs more clarity.

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Implementation details | Design becomes code spec |
| Missing alternatives | Appears like first idea |
| No context | Reviewers can't validate fit |
| Hidden complexity | Surprises during implementation |
| Scope ambiguity | Endless feature additions |
