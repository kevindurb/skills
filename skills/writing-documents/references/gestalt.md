# Writing Gestalt Documents

Re-hydrate understanding. Enable good instincts.

## Purpose

A gestalt document gives someone enough context to understand a system, concept, or domain without reading everything. After reading, they should be able to make reasonable decisions—not just navigate to other documents.

## Structure

```markdown
# [Topic]

[One paragraph: essential essence. What this is, why it matters, the key insight.]

## Core Concepts

[2-4 concepts that unlock understanding. Not a comprehensive list—the minimal set.]

### [Concept 1]
[Brief explanation with one concrete example]

### [Concept 2]
[Brief explanation with one concrete example]

## Key Relationships

[How the core concepts interact. A simple diagram if helpful.]

## Where to Go Deeper

- [Reference] for detailed specifications
- [Flow] for process understanding
- [Design] for architectural decisions
```

## Principles

**Essential, not exhaustive**: Include only what's necessary to understand. Everything else is noise that dilutes the signal.

**Concepts over details**: Teach the mental model. Details belong in reference documents.

**Concrete examples**: Abstract concepts need grounding. One good example beats three paragraphs of explanation.

**Pointers, not duplication**: Link to depth rather than copying it. Duplication drifts and creates reconciliation burden.

## Test

After reading your gestalt document, can someone:
- Explain the topic in their own words?
- Make reasonable decisions about related problems?
- Know where to look for specific details?

If they can only navigate to other documents, you wrote a table of contents, not a gestalt.

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Comprehensive coverage | Becomes reference document |
| No examples | Remains abstract, doesn't stick |
| Duplicated depth | Creates maintenance burden |
| Missing relationships | Concepts float without context |
