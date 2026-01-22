---
name: writing-documents
description: Guides effective documentation creation for humans and agents. Use when writing READMEs, guides, research, designs, plans, runbooks, or any documentation. Prevents cascading harm from wrong information.
---

# Writing Documents

Wrong information is worse than missing information. One fabricated fact becomes gospel for every future agent. Prevent harm first, enable quality second.

---

## What Kind of Document?

| If the reader wants to... | Write a... | Key insight |
|---------------------------|------------|-------------|
| Understand something | **gestalt** | Essential essence, not everything |
| Look something up | **reference** | Data in CSV, guidance in markdown |
| Inform a decision | **research** | Synthesis without prescription |
| Know how to build it | **design** | "Yep, that will work" before code |
| Know what to build next | **plan** | Reviewed by humans, implemented by agents |
| See a process end-to-end | **flow** | Stages, actors, handoffs |
| Get a question answered | **findings** | Answer before evidence |
| Carry wisdom forward | **concepts** | Capsule format |
| Follow a procedure | **process** | High-agency (outcomes) or low-agency (steps) |

Each type has guidance in `references/`. Read the relevant guide before writing.

---

## Before Writing

### Audience and Purpose

```yaml
---
description: One sentence - what this is and why it exists
tags: [searchable, terms]
audience: { human: 60, agent: 40 }
purpose: { gestalt: 0, reference: 0, research: 0, design: 0, plan: 0, flow: 0, findings: 0, concepts: 0, process: 0 }
---
```

Distribute 100 points for audience and 100 for purpose. Dominant purpose determines which guidance to follow.

**Required**: Read audience guidance before writing:
- `references/audience-agent.md` — if agent-heavy
- `references/audience-human.md` — if human-heavy

---

## Hard Rules

### Only Record What You Can Verify

Evidence hierarchy:
1. Code — directly observed
2. Docs — stated in documentation
3. Synthesis — derived from verified sources
4. User — confirmed by expert
5. Intuition — feels right, but can't prove it

### When in Doubt, Omit

Missing prompts research. Wrong causes bad decisions.

### Never Write

| Pattern | Problem |
|---------|---------|
| Timestamps | Git tracks; becomes misleading |
| "Currently" | Will become false |
| "Planned for" | Plans change |
| Estimates | Always wrong |
| Speculation about intent | Often wrong |

Mark gaps honestly: `**STUB** - needs expert input`

---

## Purpose Summaries

### Gestalt
Re-hydrate understanding. Essential essence in first paragraph. 2-4 concepts that unlock understanding. Pointers to depth, not duplication.
> `references/gestalt.md`

### Reference
Data in CSV. Guidance in markdown. Enumerate finite sets; teach discovery for infinite sets. Every entry needs "When NOT to use."
> `references/reference.md`

### Research
Synthesis without prescription. "Fastest in benchmarks" is synthesis. "You should use X" is prescription.
> `references/research.md`

### Design
Enables "Yep, that will work" before code. Establish north star. Contains complexity, brings flows and research together.
> `references/design.md`

### Plan
Reviewed by humans. Implemented by agents. Specific scope and done criteria, implementation left to judgment. Delete when complete.
> `references/plan.md`

### Flow
Stages, actors, handoffs. Descriptive, not prescriptive. Use before design to find cross-cutting concerns.
> `references/flow.md`

### Findings
Answer the question first. Evidence supports the answer. No speculation, no timelines, no unsolicited recommendations.
> `references/findings.md`

### Concepts
Crystallized wisdom in capsule format. Invariant forces precision—if you can't compress to one line, you may not understand it yet.
> `references/capsules.md`

### Process
**High-agency**: Prescribe outcomes, trust agent to fill gaps.
**Low-agency**: Skip or reorder causes harm. Scripted steps with verification.
> `references/process.md`

---

## How Documents Support Each Other

```
research --> flow --> design --> plan --> code
              ^
          concepts
```

| Document | Feeds into | When to use |
|----------|------------|-------------|
| research | flow, design, ambient knowledge | Exploring options |
| flow | design | Mapping processes |
| concepts | design | Crystallizing wisdom |
| design | plan | Defining architecture |
| plan | code | Scoping work |
| gestalt | any stage | Re-hydrating understanding |
| reference | any stage | Looking up facts |
| findings | any stage | Answering questions |

A design without flow misses how it will be used. A plan without design lacks grounding.

---

## After Writing

### Rewrite as Cohesive Whole

Edits accumulate. Each patch respects existing structure even when structure no longer serves content.

**The technique**:
1. Read the original fully
2. Replace content with placeholder
3. Write fresh what it should be, not what it was

---

## Checklist

- [ ] Frontmatter complete with audience and purpose scores
- [ ] Dominant purpose guidance read and followed
- [ ] Only verified information; gaps marked honestly
- [ ] No timestamps, "currently", estimates, speculation
- [ ] Findable, trustworthy, maintainable
- [ ] Rewritten as cohesive whole if heavily edited

---

*Wrong information is worse than missing information.*
