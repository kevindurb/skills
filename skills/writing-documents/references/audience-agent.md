# Writing for Agents

Agents read everything. The challenge is precision, retrieval, and token efficiency.

## Core Principles

### Structure Over Prose

Structured formats parse faster and more reliably than equivalent prose.

| Format | When to use |
|--------|-------------|
| Tables | Comparisons, attributes, decisions |
| Bullets | Unordered items, lists |
| Capsules | Concepts and wisdom |
| Prose | Complex reasoning that resists tabulation |

### Explicit Over Implicit

State relationships directly. Don't require inference from context.

**Bad**: Describes A, then B, expects reader to see dependency.
**Good**: A depends on B for X.

- Name the relationship: depends, triggers, blocks, contains
- Avoid ambiguous antecedents: it, this, that
- If something is NOT true, say so explicitly

### Reference Over Repetition

Point to information once defined. Never duplicate within context.

- Duplication wastes tokens
- Inconsistent duplicates create reconciliation burden
- Canonical location for each concept

### Precise Naming

Use consistent, searchable names that tokenize efficiently.

**Good**: `CircuitBreaker`, `RetryPolicy`, `IdempotencyKey`
**Bad**: circuit-breaker, retry_policy, "the idempotency mechanism"

- CamelCase for concept names (fewer tokens)
- Same term everywhere for same thing
- No synonyms—pick one name

### Evidence Hierarchy

Mark confidence levels so readers can weight information appropriately.

| Level | Confidence |
|-------|------------|
| Code | High — directly observed |
| Docs | Medium-high — stated explicitly |
| Synthesis | Medium — derived from sources |
| Expert | Medium — confirmed by human |
| Intuition | Low — mark explicitly |

Unmarked information is assumed verified.

### Boundaries Explicit

State what something is NOT and when NOT to use it.

Every reference entry needs both:
- **Use for**: [conditions]
- **Don't use for**: [conditions]

### Progressive Disclosure

Present gestalt first; reveal depth on demand via references.

- Reduces context load—agent loads only what's needed
- Gestalt enables navigation; references enable execution
- Links as selective loading mechanism

---

## Document Structure for Agents

### Three-Segment Pattern

**Beginning (Frame)**
- What is this, what problem it solves
- Key constraints, scope boundaries
- Primacy effect: early content frames interpretation of everything after

**Middle (Retrieval)**
- Structured for finding specific facts
- Consistent patterns: tables, capsules, entries
- Headers that work as search keys

**End (Synthesis)**
- How pieces fit together
- Checklists for actions
- Explicit boundaries
- Recency effect: final content most accessible during output generation

### Chunking

Size documents to be safe alone while enabling progressive disclosure.

- Each document must be safe to use without reading sister documents
- Bad outcomes from not reading related docs = chunked wrong
- Size for the task: gestalt for orientation, reference for execution

### Large Data

Tables over ~20 rows belong in linked CSV files that agents can query with tools.

---

## What Hinders Agents

| Pattern | Problem |
|---------|---------|
| Ambiguity | Multiple interpretations require guessing |
| Inconsistent terminology | Forces tracking of synonym mappings |
| Buried key facts | May not weight appropriately |
| Redundancy | Wastes context; inconsistent copies worse |
| Missing context | Unstated assumptions cause misapplication |
| Temporal markers | "Currently" becomes stale |
| Decorative formatting | Adds tokens without meaning |

---

## Checklist

- [ ] Structure used where data permits
- [ ] Relationships explicit and named
- [ ] No duplication; references to canonical locations
- [ ] Consistent precise names throughout
- [ ] Confidence levels marked for synthesis/intuition
- [ ] Boundaries stated: what it is NOT, when NOT to use
- [ ] Progressive disclosure with clear paths to depth
- [ ] Large tables linked as files, not embedded
- [ ] End section synthesizes and bounds
