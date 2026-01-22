# Writing Concept Capsules

Crystallized wisdom in token-efficient format.

## Purpose

Capsules capture hard-won insights in a format that's precise, composable, and easy for both humans and agents to apply. The constraint of compression forces clarity—if you can't compress it, you may not understand it yet.

## Structure

```markdown
## Capsule: [ConceptName]

**Invariant**
[The core truth in ≤30 tokens. What is ALWAYS true about this concept.]

**Example**
[Concrete scenario showing the invariant in action. Brief.]

//BOUNDARY: [When this does NOT apply. The edge of validity.]

**Depth**
- [Supporting detail]
- [Supporting detail]
- [How to apply this]
```

## Principles

**Invariant is everything**: The invariant must be true in all cases within the boundary. If you can find an exception, narrow the boundary or refine the invariant.

**30 token constraint**: Forces precision. Verbose invariants hide fuzzy thinking.

**Boundaries prevent misapplication**: Every concept has limits. State them explicitly.

**Composable**: Agents can select and combine capsules without averaging conflicting ideas because boundaries make applicability clear.

**CamelCase naming**: Names become retrieval keys. `TokenEfficiency` not "token efficiency."

## Examples

### Good Capsule

```markdown
## Capsule: StructureOverProse

**Invariant**
Structured formats parse faster and more reliably than equivalent prose.

**Example**
Comparison as prose: 200 words, ambiguous relationships.
Same comparison as table: 50 tokens, relationships explicit.

//BOUNDARY: Prose for complex reasoning that resists tabulation.

**Depth**
- Tables for comparisons, attributes
- Bullets for lists
- Prose only when relationships are too complex for structure
```

### Bad Capsule

```markdown
## Capsule: good-writing

**Invariant**
Good documentation is clear and helps readers understand things better
by explaining concepts in ways that make sense to them.

**Example**
When you write clearly, people understand.

**Depth**
- Be clear
- Help readers
```

Problems: vague invariant (45+ tokens, no testable claim), weak example, no boundary, no CamelCase.

## Test

Can you apply the invariant mechanically to a new situation and get a correct answer? If applying it requires judgment about what it means, the invariant isn't precise enough.

## Anti-patterns

| Pattern | Problem |
|---------|---------|
| Long invariant | Fuzzy thinking |
| No boundary | Overapplication |
| Abstract example | Doesn't ground concept |
| Platitudes | No actionable insight |
| Lowercase name | Poor retrieval |
