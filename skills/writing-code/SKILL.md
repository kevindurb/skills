---
name: writing-code
description: Guidance for writing high-quality code. Use when writing any code—functions, classes, scripts, fixes, features, tests. Applies to all languages and all code sizes, from one-liners to modules.
---

# Writing Code

Code is read far more often than written. Optimize for the reader.

---

## Core Question

**Does this make future changes easier or harder?**

---

## Priority When Conflicts Arise

1. **Correctness** — Must work
2. **Readability** — Must be understood quickly
3. **Simplicity** — Minimal complexity
4. **Testability** — Can verify in isolation
5. **Performance** — Only optimize measured hotspots

---

## Before Writing

1. Read nearby code first
2. Match existing conventions
3. Only what's needed—nothing speculative

---

## Quick Checks

| Area | Check |
|------|-------|
| Names | Reveal intent? (`daysSinceModification` not `d`) |
| Functions | Small? (<20 lines ideal, >50 split immediately) |
| Nesting | Shallow? (≤3 levels, use guard clauses) |
| Comments | Explain *why*, not *what*? |
| Errors | Validated at boundaries? Fail fast? |

---

## Red Flags (Stop and Fix)

- Method >50 lines
- Nesting >3 levels
- Boolean parameters: `createUser(true, false)`
- Magic numbers: `if (status == 7)`
- Train-wreck chaining: `a.b().c().d().e()`
- Generic catch-all exception handlers
- Code needs comments to explain *what* it does

---

## Key Insight

**"Duplication is far cheaper than the wrong abstraction."** — Sandi Metz

Three similar lines > premature abstraction. Wait for three instances.

---

## Reference Material

- `references/naming.md` — Names are the most impactful factor
- `references/functions.md` — Size, responsibility, arguments
- `references/readability-patterns.md` — Guard clauses, explanatory variables
- `references/quality-metrics.md` — Objective thresholds

---

*Optimize for the reader.*
