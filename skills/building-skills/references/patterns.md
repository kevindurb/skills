# Skill Patterns

Proven patterns for effective skills.

---

## Workflow Patterns

### Checklist Progress

Give Claude trackable progress through multi-step workflows.

```markdown
## Processing Workflow

Copy and track progress:
- [ ] Step 1: Gather context
- [ ] Step 2: Analyze inputs
- [ ] Step 3: Generate output
- [ ] Step 4: Validate results
- [ ] Step 5: Present findings
```

### Feedback Loop

Prevent cascade failures with immediate validation.

```markdown
## Edit Process

1. Make changes
2. **Validate immediately**: Run `npm test`
3. If validation fails → fix → validate again
4. Only proceed when validation passes

Never batch multiple changes before validating.
```

### Conditional Routing

Handle branching workflows explicitly.

```markdown
## Workflow Selection

1. Determine the modification type:

   **Creating new?** → Follow "Creation Workflow" below
   **Editing existing?** → Follow "Edit Workflow" below
   **Deleting?** → Follow "Deletion Workflow" below

## Creation Workflow
[steps]

## Edit Workflow
[steps]
```

### Gate Checks

Ensure prerequisites before proceeding.

```markdown
## Prerequisites

Before starting, verify:
- [ ] On correct branch (`main` or feature branch)
- [ ] No uncommitted changes (`git status` clean)
- [ ] Tests passing (`npm test`)

**Stop if any prerequisite fails.** Do not proceed.
```

---

## Content Patterns

### Dynamic Context Injection

Pull real-time data into skill context.

```markdown
## Current State

- Branch: !`git branch --show-current`
- Status: !`git status --short`
- Recent commits: !`git log --oneline -5`

## PR Context

- Title: !`gh pr view --json title -q .title`
- Changed files: !`gh pr diff --name-only`
```

### Argument Handling

Process user-provided arguments.

```markdown
## Input

Process: $ARGUMENTS

If no arguments provided, use the current directory.

## Handling Multiple Arguments

Arguments: $ARGUMENTS

Parse as space-separated list. Process each in order.
```

### Reference Linking

Keep main skill concise with linked references.

```markdown
# Quick Start

[Essential 20% that handles 80% of cases]

## Edge Cases

See [edge-cases.md](references/edge-cases.md) for unusual scenarios.

## Advanced Configuration

See [advanced.md](references/advanced.md) for power user options.
```

---

## Safety Patterns

### Confirmation Gates

Require explicit confirmation for dangerous operations.

```markdown
## Deployment

1. Show deployment plan
2. **Ask user**: "Proceed with deployment to production? (yes/no)"
3. Only continue if user confirms "yes"

Never auto-proceed with production deployments.
```

### Dry Run First

Preview changes before applying.

```markdown
## Process

1. **Dry run**: Show what would change (no modifications)
2. Present changes to user
3. If user approves, apply changes
4. Verify applied correctly
```

### Rollback Documentation

Always provide escape hatches.

```markdown
## Rollback

If something goes wrong:

1. [Immediate mitigation step]
2. [How to undo changes]
3. [How to restore previous state]

Keep this section visible—don't bury it.
```

---

## Output Patterns

### Structured Findings

Consistent format for review-type skills.

```markdown
## Output Format

Present findings in three categories:

### Critical (must fix)
- [Issue]: [Location] — [Why it matters]

### Important (should address)
- [Issue]: [Location] — [Suggestion]

### Suggestions (nice to have)
- [Improvement]: [Location] — [Benefit]
```

### Summary First

Front-load the key information.

```markdown
## Output Structure

1. **One-line summary**: The key finding/result
2. **Key points**: 3-5 bullets of important details
3. **Details**: Full analysis (for those who want depth)

Reader should get value from just the summary.
```

---

## Anti-Patterns to Avoid

| Anti-Pattern | Problem | Fix |
|--------------|---------|-----|
| Implicit state | Assumes context not guaranteed | Gather state explicitly |
| Silent failures | Errors go unnoticed | Validate after each step |
| Unbounded loops | Can run forever | Add max iteration limits |
| Magic values | Hardcoded paths, names | Use arguments or env vars |
| Prose instructions | Hard to follow precisely | Use numbered steps, bullets |
| Missing boundaries | Unclear when to stop | Define explicit exit conditions |

---

## Composition Patterns

### Skill Chaining

Reference other skills for combined workflows.

```markdown
## Process

1. Invoke `writing-documents` skill for documentation standards
2. Apply those standards to this task
3. [Skill-specific steps]
```

### Shared References

Multiple skills can reference common guidance.

```
skills/
├── code-review/
│   └── SKILL.md → references ../shared/conventions.md
├── pr-create/
│   └── SKILL.md → references ../shared/conventions.md
└── shared/
    └── conventions.md
```

### Layered Complexity

Simple default, advanced optional.

```markdown
## Quick Mode (default)

[Fast path for common cases]

## Thorough Mode

If user specifies "thorough" in arguments:
[Extended analysis with more checks]
```
