---
name: building-skills
description: Creates Claude Code skills with proper structure, frontmatter, and documentation. Use when building new skills, scaffolding skill directories, or improving existing skills.
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash(mkdir:*)
  - Bash(ls:*)
---

# Building Skills

**First**: Invoke the `writing-documents` skill. Skills are documentation for agents—the same principles apply.

---

## Skill Anatomy

```
skill-name/
├── SKILL.md              # Required: main instructions (<500 lines)
├── references/           # Optional: detailed guidance
│   ├── patterns.md
│   └── examples.md
├── templates/            # Optional: structures to fill
└── scripts/              # Optional: executable utilities
```

**Directory name becomes the slash command**: `.claude/skills/code-review/` creates `/code-review`.

---

## SKILL.md Structure

```yaml
---
name: skill-name                    # Slash command (required)
description: What it does and when  # Trigger-rich (recommended)
allowed-tools:                      # Restrict capabilities (optional)
  - Read
  - Grep
disable-model-invocation: true      # User-only for side effects
user-invocable: false               # Claude-only for background knowledge
context: fork                       # Isolated subagent execution
agent: Explore                      # Subagent type
model: claude-sonnet-4-5-20250929   # Override model
---

# Skill Title

[Instructions Claude follows when skill is invoked]
```

---

## Frontmatter Reference

| Field | Purpose | When to use |
|-------|---------|-------------|
| `name` | Slash command (max 64 chars, lowercase/hyphens) | Always |
| `description` | Helps Claude auto-invoke | Always—be trigger-rich |
| `allowed-tools` | Restrict available tools | Read-only exploration, safety |
| `disable-model-invocation` | Only user can invoke | Deployments, commits, side effects |
| `user-invocable: false` | Hidden from menu, Claude-only | Background knowledge |
| `context: fork` | Run in isolated subagent | Complex independent workflows |
| `agent` | Subagent type (Explore, Plan) | With `context: fork` |
| `model` | Override model used | When specific model needed |

---

## Dynamic Content

### Shell Preprocessing
```markdown
Current branch: !`git branch --show-current`
PR diff: !`gh pr diff`
```
Commands run before content reaches Claude. Output replaces placeholder.

### Arguments
```markdown
Process this file: $ARGUMENTS
```
`/skill-name foo.txt` sends "Process this file: foo.txt" to Claude.

### Session Variables
```markdown
Session: ${CLAUDE_SESSION_ID}
```

---

## Two Skill Types

### Knowledge Skills (Reference)
Background information Claude applies to work.

```yaml
---
name: api-conventions
description: REST API design patterns for this project
user-invocable: false
---
```

- Style guides, conventions, domain knowledge
- Information Claude can't infer from code
- Often `user-invocable: false`—Claude loads when relevant

### Workflow Skills (Task)
Step-by-step procedures for specific actions.

```yaml
---
name: deploy
description: Deploy to production environment
disable-model-invocation: true
allowed-tools:
  - Bash(git:*)
  - Bash(gh:*)
---
```

- Deployments, code generation, testing
- Often `disable-model-invocation: true` for side effects
- May use `context: fork` for isolation

---

## Writing Trigger-Rich Descriptions

The description determines when Claude auto-invokes. Include:

- What the skill does
- When to use it
- Specific file types, action verbs, use cases

**Good**:
```yaml
description: Analyze Excel spreadsheets, create pivot tables, generate charts.
  Use when working with .xlsx files, spreadsheet data, or tabular analysis.
```

**Bad**:
```yaml
description: Helps with documents
```

---

## Invocation Control Matrix

| Want | Set |
|------|-----|
| Both user and Claude can invoke | (default) |
| User only (side effects) | `disable-model-invocation: true` |
| Claude only (background) | `user-invocable: false` |
| Neither auto-invokes | Both flags true |

---

## Progressive Disclosure

Keep SKILL.md under 500 lines. Move detailed content to `references/`:

```markdown
# Quick Start
[Essential guidance]

## Advanced
See [patterns.md](references/patterns.md) for complex cases.
```

Claude loads full SKILL.md when activated—conciseness impacts token efficiency.

---

## Patterns That Work

### Workflow Checklists
```markdown
## Process
- [ ] Step 1: Analyze
- [ ] Step 2: Generate
- [ ] Step 3: Validate
```

### Feedback Loops
```markdown
1. Make changes
2. **Validate**: Run tests
3. If failed → fix → validate again
4. Only proceed when passing
```

### Conditional Routing
```markdown
## Workflow
1. Determine type:
   **New?** → Creation workflow
   **Existing?** → Edit workflow
```

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Vague description | Add specific triggers, file types, verbs |
| Over 500 lines | Move detail to `references/` |
| Missing `disable-model-invocation` on side effects | Add flag for deploys, commits, pushes |
| Windows paths (`\`) | Use forward slashes (`/`) |
| Assuming tools installed | Document dependencies |
| Time-sensitive content | Remove dates, "currently" |

---

## Checklist

- [ ] Directory name matches intended slash command
- [ ] `name` field is lowercase with hyphens
- [ ] `description` is trigger-rich (what + when + specifics)
- [ ] SKILL.md under 500 lines
- [ ] Side-effect skills have `disable-model-invocation: true`
- [ ] `allowed-tools` restricts capabilities appropriately
- [ ] References in separate files, not inline
- [ ] No time-sensitive information
- [ ] Tested that skill actually invokes when relevant

---

## Creating a New Skill

1. **Clarify purpose**: Knowledge or workflow? What triggers it?
2. **Invoke writing-documents**: Skills are agent documentation
3. **Create structure**:
   ```bash
   mkdir -p .claude/skills/skill-name/references
   ```
4. **Write SKILL.md**: Frontmatter + instructions (<500 lines)
5. **Add references**: Detailed guidance in separate files
6. **Test activation**: Describe relevant task, verify skill loads

---

*Skills are documentation with frontmatter. Apply writing-documents principles.*
