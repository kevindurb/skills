---
name: using-skills
description: Encourages checking and using available skills before starting work. Invoke at the start of any task to ensure relevant skills are loaded.
---

# Using Skills

Before starting any task, check your available skills. Skills encode proven practices—ignoring them means reinventing wheels or missing important patterns.

---

## Available Skills

| Skill | Invoke when... | Key insight |
|-------|----------------|-------------|
| `writing-code` | Writing functions, classes, scripts, fixes, features, tests | Correctness > readability > simplicity |
| `writing-documents` | Writing READMEs, guides, designs, plans, runbooks, any docs | Wrong info worse than missing info |
| `building-skills` | Creating or improving Claude Code skills | Skills are agent docs—invokes `writing-documents` |
| `code-review` | Reviewing PRs, commits, or staged changes | Run via **Task tool** to save tokens |
| `review-responder` | Processing review feedback (GitHub comments, code-review output) | Walks through changes one-by-one |

---

## Quick Match

| Task | Skill |
|------|-------|
| Write a function | `writing-code` |
| Create documentation | `writing-documents` |
| Design a feature | `writing-documents` (design type) |
| Review a PR | `code-review` via Task tool |
| Address review feedback | `review-responder` |
| Build a new skill | `building-skills` |

---

## Process

1. **Check the table above** — Which skills match your task?
2. **Invoke relevant skills** — Load them before starting work
3. **Apply their guidance** — Follow the patterns they establish

---

## When in Doubt, Invoke

If there's even a small chance a skill applies, invoke it. The cost of loading an irrelevant skill is low. The cost of missing relevant guidance is high.

Skills compose. One skill may tell you to invoke another.
