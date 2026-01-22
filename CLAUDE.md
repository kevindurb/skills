# Personal Skills Plugin

Claude Code plugin repository for portable agent skills. Skills here are general-purpose and not tied to specific projects.

## Available Skills

| Skill | Purpose | Invoke when |
|-------|---------|-------------|
| `writing-documents` | Documentation guidance | Writing READMEs, guides, designs, plans, runbooks, any documentation |
| `building-skills` | Skill creation | Creating or improving Claude Code skills |
| `code-review` | Code change review | Reviewing PRs, commits, or staged changes (runs as agent fork) |

## Repository Structure

```
skills/
├── [skill-name]/
│   ├── SKILL.md           # Required: main instructions
│   └── references/        # Optional: detailed guidance
```

Each subdirectory under `skills/` is a complete skill. Directory name becomes the skill identifier.

## Adding Skills

1. Create directory: `skills/[skill-name]/`
2. Add `SKILL.md` with frontmatter and instructions
3. Add `references/` for detailed guidance if needed
4. Plugin auto-discovers skills from directory structure

## Key Patterns

### writing-documents
- **Evidence hierarchy**: Code > Docs > Synthesis > Expert > Intuition
- **Document types**: gestalt, reference, research, design, plan, flow, findings, concepts, process
- **Hard rule**: Wrong information is worse than missing information

### building-skills
- **Knowledge skills**: Background information, often `user-invocable: false`
- **Workflow skills**: Procedures with side effects, often `disable-model-invocation: true`
- Skills are documentation for agents—invoke `writing-documents` first

### code-review
- **Agent fork**: Runs in isolated context via `context: fork` to save tokens in main conversation
- **Output for humans**: Review is a findings document—invokes `writing-documents`
- **Priority order**: Correctness > Security > Architecture > Performance > Tests > Style

## Installation

```bash
claude plugins add /path/to/skills
```

Skills become available as `personal-skills:[skill-name]`.
