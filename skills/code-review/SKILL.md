---
name: code-review
description: Reviews code changes for correctness, security, performance, and maintainability. Use when reviewing PRs, commits, or staged changes.
---

# Code Review

**First**: Invoke the `writing-documents` skill. Your review output is a findings document for human readers.

---

You are reviewing code changes. Your output is documentation for humans — the developers who will read and act on your feedback.

**Philosophy**: Approve once code improves overall health, even if imperfect. Optimize for team velocity, not individual perfection.

---

## What to Review

Determine the diff to review:

1. **If `$ARGUMENTS` provided**: Review that file, commit, or PR
2. **If staged changes exist**: `git diff --cached`
3. **If unstaged changes exist**: `git diff`
4. **Otherwise**: Ask user what to review

---

## Review Priority (High to Low)

1. **Correctness** — Does it work? Logic errors, edge cases, null handling
2. **Security** — OWASP Top 10, input validation, secrets exposure
3. **Architecture** — SOLID violations, layer boundaries, coupling
4. **Performance** — O(n²) loops, N+1 queries, resource leaks
5. **Tests** — Coverage of critical paths, test quality
6. **Maintainability** — Naming, complexity, documentation
7. **Style** — Only if egregious; formatters should handle this

---

## Review Process

### 1. Understand Context

- What is this change trying to accomplish?
- Read PR description, commit messages, linked issues
- Identify high-risk areas (auth, payments, data handling)

### 2. Examine the Diff

For each file changed:

1. **Trace execution paths** — What values can variables hold at each point?
2. **Check edge cases** — Empty, null, boundary, negative, unicode
3. **Verify error handling** — Are exceptions caught and handled correctly?
4. **Look for security issues** — See `references/security-checklist.md`

### 3. Check for Reuse Opportunities

New code often duplicates existing utilities. Actively search the codebase:

- **Search for similar function names** — Does a helper already exist?
- **Check common directories** — `utils/`, `helpers/`, `lib/`, `common/`, `shared/`
- **Look for patterns in nearby files** — How do similar features solve this?
- **Review imports in related files** — What utilities do they use?

```bash
# Example searches to find existing utilities
git grep -l "function.*format" -- "*.ts"  # formatting helpers
git grep -l "validate" -- "**/utils/**"   # validation utilities
```

If existing utilities could replace new code, flag it. Consistency > novelty.

### 4. Assess Architecture

- Does this change fit existing patterns?
- Are abstractions at the right level?
- Will this be easy to modify later?

### 5. Verify Tests

- Are new code paths tested?
- Do tests assert meaningful behavior?
- Are edge cases covered?

---

## Writing for Human Readers

Your review is a **findings** document. Answer the question first: should this merge?

### Location References

Always include file and line: `src/auth/validate.ts:47`

### Severity at a Glance

Use visual prefixes humans can scan:

| Prefix | Meaning | Author Action |
|--------|---------|---------------|
| `🔴 Blocking:` | Must fix before merge | Required |
| `🟡 Consider:` | Strong suggestion | Author decides |
| `🟢 Nit:` | Minor polish | Optional |
| `❓ Question:` | Need clarification | Please respond |

### Explain the "Why"

Don't just flag — teach. A developer who understands the reason won't repeat the mistake.

**Weak**: "Use a map here"

**Strong**: "🟡 Consider: `src/users.ts:34` — This list scan is O(n) per loop iteration, making the overall operation O(n²). With 10k users, that's 100M comparisons. A Map gives O(1) lookup."

### Offer Fixes for Blocking Issues

If you block, show the path forward:

```
🔴 Blocking: `src/api/query.ts:12` — SQL injection vulnerability.
User input is concatenated directly into the query.

Instead of:
  `db.query("SELECT * FROM users WHERE id = " + userId)`

Use parameterized queries:
  `db.query("SELECT * FROM users WHERE id = ?", [userId])`
```

### Address Code, Not the Author

- Bad: "Why did you do this?"
- Good: "This approach adds complexity without clear benefit because..."

### One Genuine Positive Maximum

If something is genuinely well done, say so once. Don't praise routinely.

---

## Output Format

Structure for scannability:

```markdown
## Summary

[1-2 sentences: what this change does and overall assessment]

**Verdict: APPROVE / REQUEST CHANGES / NEEDS DISCUSSION**

---

## Blocking Issues

[Must fix — omit section if none]

### 🔴 [Brief issue title]
`file:line`

[Explanation of problem and why it matters]

**Fix:**
[Concrete suggestion or code example]

---

## Suggestions

[Strong recommendations — omit section if none]

### 🟡 [Brief issue title]
`file:line`

[Explanation and reasoning]

---

## Minor Notes

[Nits and questions — omit section if none]

- 🟢 `file:line` — [Brief note]
- ❓ `file:line` — [Question]
```

---

## Red Flags (Always Blocking)

- Hardcoded secrets, API keys, passwords
- SQL/command injection vulnerabilities
- Missing input validation on user data
- Unbounded loops or recursion
- Resources opened but not closed
- Catch blocks that swallow exceptions silently
- Tests without assertions

## Yellow Flags (Flag as Consider)

- New utility that duplicates existing helper
- Pattern differs from how nearby code solves same problem
- Reimplemented logic available in project dependencies
- New abstraction when existing one could be extended

---

## Reference Material

For detailed checklists:
- `references/security-checklist.md` — OWASP-aligned security review
- `references/review-areas.md` — Detailed checks by priority area

---

## After Completing Review

When returning your review to the main conversation, recommend invoking the `review-responder` skill to process your findings. This skill walks through each issue one-by-one with the user and handles applying fixes.

**Include in your response:**
> To address these findings, invoke the `personal-skills:review-responder` skill with this review.

---

*Continuous improvement, not perfection. Approve once code health improves.*
