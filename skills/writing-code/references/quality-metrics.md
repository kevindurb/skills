# Quality Metrics

Objective thresholds for code quality.

---

## Complexity

| Metric | Good | Warning | Critical |
|--------|------|---------|----------|
| Cyclomatic Complexity | ≤10 | 11-20 | >20 |
| Cognitive Complexity | ≤15 | 16-25 | >25 |
| Method Length (lines) | <20 | 20-50 | >50 |
| Class Length (lines) | <200 | 200-500 | >500 |
| Nesting Depth | ≤3 | 4 | >4 |

**Cyclomatic complexity**: Count of linearly independent paths. High = hard to test.

**Cognitive complexity**: Measures human understanding difficulty. High = hard to change safely.

---

## Test Coverage

| Metric | Target | Minimum |
|--------|--------|---------|
| Line Coverage | ≥80% | 60% |
| Branch Coverage | ≥70% | 50% |
| Critical Path Coverage | ≥90% | 80% |

Coverage measures execution, not assertion quality. Tests without meaningful assertions inflate coverage without value.

---

## Duplication

| Metric | Good | Warning | Critical |
|--------|------|---------|----------|
| Code Duplication | <3% | 3-5% | >5% |

Note: Incidental duplication (same code, different concepts) is acceptable.

---

## Technical Debt

| Rating | Debt Ratio |
|--------|------------|
| A | ≤5% |
| B | 5-10% |
| C | 10-20% |
| D | >20% |

Debt ratio = remediation cost / development cost.

---

## Function Arguments

| Count | Rating |
|-------|--------|
| 0-1 | Ideal |
| 2 | Acceptable |
| 3 | Needs justification |
| 4+ | Refactor |
