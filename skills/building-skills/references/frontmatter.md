# Frontmatter Reference

Complete reference for SKILL.md frontmatter fields.

---

## Required Fields

### name

Slash command name. Lowercase letters, numbers, hyphens only. Max 64 characters.

```yaml
name: code-review
```

Directory name is used if omitted, but explicit is clearer.

---

## Recommended Fields

### description

How Claude decides when to auto-invoke. Max 1024 characters.

**Structure**: What it does + when to use + specific triggers

```yaml
description: Reviews pull requests for code quality and security issues.
  Use when reviewing PRs, before merging, or when asked to check changes.
  Works with GitHub PRs via gh CLI.
```

**Trigger elements**:
- Action verbs: review, analyze, generate, deploy, test
- File types: .tsx, .py, Excel, PDF
- Tools: GitHub, Docker, npm
- Contexts: PR, commit, branch, production

---

## Invocation Control Fields

### disable-model-invocation

When `true`, only explicit user commands (`/skill-name`) invoke the skill. Claude cannot auto-invoke.

```yaml
disable-model-invocation: true
```

**Use for**: Deployments, git pushes, sending messages, any side effects.

### user-invocable

When `false`, skill is hidden from the slash command menu. Claude can still auto-invoke based on description.

```yaml
user-invocable: false
```

**Use for**: Background knowledge, conventions, domain context that isn't a direct command.

---

## Tool Restriction Fields

### allowed-tools

Restricts which tools the skill can use. Accepts list or comma-separated string.

```yaml
# List format (recommended)
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash(git:*)

# String format
allowed-tools: Read, Grep, Glob
```

**Common patterns**:

| Pattern | Tools |
|---------|-------|
| Read-only exploration | `Read, Grep, Glob` |
| Git operations | `Bash(git:*)` |
| GitHub CLI | `Bash(gh:*)` |
| File editing | `Read, Write, Edit` |

**Glob syntax for Bash**:
- `Bash(git:*)` — any git command
- `Bash(npm:*)` — any npm command
- `Bash(docker build:*)` — docker build only

---

## Execution Context Fields

### context

Set to `fork` for isolated subagent execution.

```yaml
context: fork
```

**Effects**:
- Skill content becomes subagent's task
- No access to conversation history
- Results summarize back to main session
- Enables focused, independent work

### agent

Subagent type when using `context: fork`.

```yaml
context: fork
agent: Explore
```

**Options**:
- `Explore` — Read-only codebase exploration
- `Plan` — Planning and analysis
- `general-purpose` — Full capabilities

### model

Override the model used for this skill.

```yaml
model: claude-sonnet-4-5-20250929
```

**Use for**: When specific model capabilities needed, cost optimization.

---

## Combination Patterns

### Read-only Explorer

```yaml
---
name: architecture-review
description: Analyzes system architecture and dependencies
context: fork
agent: Explore
allowed-tools:
  - Read
  - Grep
  - Glob
---
```

### Protected Deployment

```yaml
---
name: deploy-production
description: Deploy to production servers
disable-model-invocation: true
allowed-tools:
  - Bash(git:*)
  - Bash(docker:*)
---
```

### Background Knowledge

```yaml
---
name: api-conventions
description: REST API design patterns for this codebase
user-invocable: false
---
```

### Full Workflow

```yaml
---
name: pr-review
description: Reviews PRs for quality, security, maintainability
context: fork
agent: Explore
disable-model-invocation: true
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash(gh:*)
---
```

---

## Validation

| Field | Constraint |
|-------|------------|
| `name` | Max 64 chars, `[a-z0-9-]` only |
| `description` | Max 1024 chars |
| `allowed-tools` | Valid tool names |
| `agent` | Explore, Plan, or general-purpose |
| `context` | Only `fork` supported |
