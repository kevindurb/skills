# Writing Reference Documents

Data in CSV. Guidance in markdown.

## Purpose

Reference documents are looked up, not read. Optimize for finding specific information quickly.

## Structure

```markdown
# [Topic] Reference

[One sentence: what this reference covers]

## [Category A]

### [Entry 1]
- **What**: [Brief description]
- **When to use**: [Conditions]
- **When NOT to use**: [Boundaries]
- **Example**: [Concrete usage]

### [Entry 2]
...

## [Category B]
...

## Quick Reference Table

| Entry | Purpose | Common Use |
|-------|---------|------------|
| ... | ... | ... |
```

## Principles

**Enumerate finite sets**: If there are 12 error codes, list all 12. Don't make readers search.

**Teach discovery for infinite sets**: If there are unlimited configurations, explain how to find and understand them.

**Every entry needs boundaries**: "When to use" is incomplete without "When NOT to use." Readers misapply guidance when boundaries aren't explicit.

**Consistent structure**: Same format for every entry. Predictable structure enables scanning.

**Large data in CSV**: Tables over ~20 rows belong in linked CSV files that tools can query.

## Test

Can someone find what they need in under 30 seconds? If they have to read prose to locate information, the structure has failed.

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Prose explanations | Slows lookup |
| Missing boundaries | Causes misapplication |
| Incomplete enumeration | Forces external search |
| Inconsistent entry format | Breaks scanning |
| Huge inline tables | Bloats documents, hard to query |
