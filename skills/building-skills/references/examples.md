# Skill Examples

Complete examples demonstrating different skill types.

---

## Knowledge Skill: API Conventions

Background knowledge Claude applies when relevant.

```yaml
---
name: api-conventions
description: REST API design patterns and conventions for this project.
  Apply when creating endpoints, reviewing API code, or discussing API design.
user-invocable: false
---

# API Conventions

## Endpoint Naming

- Resources are nouns: `/users`, `/posts`, `/comments`
- Actions are verbs: `/posts/{id}/publish`, `/users/{id}/activate`
- Plural for collections: `/users` not `/user`
- Lowercase with hyphens: `/user-preferences` not `/userPreferences`

## Response Format

All responses follow this structure:

```json
{
  "success": true,
  "data": { ... },
  "error": null,
  "meta": {
    "page": 1,
    "total": 100
  }
}
```

## Error Handling

- 400: Client error (validation, bad request)
- 401: Authentication required
- 403: Forbidden (authenticated but not authorized)
- 404: Resource not found
- 500: Server error (never expose internals)

## Pagination

Query params: `?page=1&limit=20`
Response includes `meta.page`, `meta.total`, `meta.hasMore`
```

---

## Workflow Skill: PR Review

User-triggered workflow with side effects.

```yaml
---
name: pr-review
description: Reviews pull requests for code quality, security issues, and
  maintainability. Use when reviewing PRs, before merging, or checking changes.
context: fork
agent: Explore
disable-model-invocation: true
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash(gh:*)
---

# Pull Request Review

## Context

- PR: !`gh pr view --json title,body,url -q '"\(.title)\n\(.url)"'`
- Files changed: !`gh pr diff --name-only`
- Additions/Deletions: !`gh pr view --json additions,deletions -q '"+\(.additions) -\(.deletions)"'`

## Review Process

- [ ] **Understand intent**: Read PR description, identify the goal
- [ ] **Review changes**: Examine each file for issues
- [ ] **Check tests**: Verify new code has appropriate test coverage
- [ ] **Validate patterns**: Ensure code follows project conventions

## What to Look For

### Critical (block merge)
- Security vulnerabilities
- Data loss risks
- Breaking changes without migration

### Important (should fix)
- Missing error handling
- Performance issues
- Missing tests for new functionality

### Suggestions (nice to have)
- Code style improvements
- Documentation updates
- Refactoring opportunities

## Output

Provide structured feedback:

**Summary**: One sentence overall assessment

**Critical Issues**:
- [File:line] — Issue description

**Important Issues**:
- [File:line] — Issue description

**Suggestions**:
- [File:line] — Suggestion

**Verdict**: Approve / Request Changes / Comment
```

---

## Workflow Skill: Deploy

Protected deployment with confirmation.

```yaml
---
name: deploy
description: Deploy application to staging or production environment.
  Use for deployments only.
disable-model-invocation: true
allowed-tools:
  - Bash(git:*)
  - Bash(docker:*)
  - Bash(kubectl:*)
---

# Deployment

## Prerequisites

Before deploying, verify:
- [ ] On `main` branch
- [ ] All tests passing
- [ ] No uncommitted changes

**Stop if any check fails.**

## Environment

Target: $ARGUMENTS (default: staging)

Valid targets: staging, production

## Process

### Staging

1. Build image: `docker build -t app:latest .`
2. Push to registry
3. Update staging deployment
4. Verify health check

### Production

1. **Confirm**: Ask user "Deploy to PRODUCTION? Type 'yes' to confirm"
2. Only proceed if user types exactly "yes"
3. Build and tag with version
4. Push to registry
5. Rolling update to production
6. Monitor for 5 minutes
7. Report deployment status

## Rollback

If deployment fails:

```bash
kubectl rollout undo deployment/app
```

Previous version will be restored within 60 seconds.
```

---

## Exploration Skill: Architecture Review

Read-only analysis in isolated context.

```yaml
---
name: architecture-review
description: Analyzes system architecture, dependencies, and structure.
  Use when understanding codebase organization or planning refactors.
context: fork
agent: Explore
allowed-tools:
  - Read
  - Grep
  - Glob
---

# Architecture Review

## Analysis Areas

1. **Directory Structure**: How is code organized?
2. **Dependencies**: What external packages are used?
3. **Entry Points**: Where does execution start?
4. **Data Flow**: How does data move through the system?
5. **Boundaries**: Where are the module boundaries?

## Process

- [ ] Map top-level directory structure
- [ ] Identify core modules and their responsibilities
- [ ] Trace key data flows
- [ ] Document external dependencies
- [ ] Note architectural patterns used

## Output

### Overview
[2-3 sentence summary of the architecture]

### Structure
```
[Directory tree of key areas]
```

### Key Components
| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| ... | ... | ... |

### Patterns Observed
- [Pattern]: [Where used]

### Potential Concerns
- [Concern]: [Why it matters]

### Recommendations
- [Recommendation]: [Expected benefit]
```

---

## Minimal Skill: Greeting

Simplest possible skill structure.

```yaml
---
name: greet
description: Provides a friendly greeting. Use when user says hello.
---

# Greeting

Respond with a warm, friendly greeting. Keep it brief and natural.

If $ARGUMENTS contains a name, personalize the greeting.
```

---

## Skill with Templates

Using template files for consistent output.

```
generate-component/
├── SKILL.md
└── templates/
    ├── component.tsx.template
    └── component.test.tsx.template
```

```yaml
---
name: generate-component
description: Generates React components with tests following project patterns.
  Use when creating new components.
allowed-tools:
  - Read
  - Write
  - Bash(mkdir:*)
---

# Generate Component

## Input

Component name: $ARGUMENTS

## Process

1. Create directory: `src/components/{ComponentName}/`
2. Generate component using [template](templates/component.tsx.template)
3. Generate test using [template](templates/component.test.tsx.template)
4. Export from index

## Templates

See `templates/` directory for component structure.

Customize template variables:
- `{ComponentName}`: PascalCase component name
- `{componentName}`: camelCase for variables
```
