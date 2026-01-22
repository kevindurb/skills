# Writing Flow Documents

Stages, actors, handoffs.

## Purpose

Flow documents describe how processes actually work—the stages, who's involved, and how work moves between them. They're descriptive (what happens) not prescriptive (what should happen).

## Structure

```markdown
# [Process] Flow

[One sentence: what process this describes]

## Actors

| Actor | Role |
|-------|------|
| [Actor 1] | [What they do in this process] |
| [Actor 2] | [What they do in this process] |

## Stages

### 1. [Stage Name]

**Actor**: [Who performs this stage]

**Trigger**: [What causes this stage to start]

**Actions**:
- [Action 1]
- [Action 2]

**Outputs**: [What this stage produces]

**Handoff to**: [Next stage]

### 2. [Stage Name]
...

## Flow Diagram

[Mermaid or ASCII diagram showing the flow]

## Edge Cases

### [Edge Case 1]
[How the flow handles this case]

## Cross-Cutting Concerns

- [Concern that affects multiple stages]
```

## Principles

**Descriptive, not prescriptive**: Document what happens, not what you wish happened. If there's a gap between reality and ideal, that's valuable information for design.

**Concrete enough to discuss**: Stages should be specific enough that stakeholders can point to problems.

**Abstract enough for flexibility**: Don't lock in implementation details. The flow should survive technical changes.

**Use before design**: Flows reveal cross-cutting concerns (auth, logging, error handling) that designs need to address.

**Actors are explicit**: Every action has someone responsible. Ambiguous ownership causes dropped handoffs.

## Test

Can stakeholders trace a real scenario through the flow? If they say "but what about X?", you've missed an edge case or stage.

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Idealized flow | Doesn't match reality |
| Missing actors | Unclear responsibility |
| No edge cases | Surprised by exceptions |
| Too detailed | Becomes implementation spec |
| No diagram | Hard to see big picture |
