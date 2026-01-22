# Readability Patterns

Practical techniques for reducing cognitive load.

---

## Guard Clauses

Eliminate nesting by handling edge cases first.

**Before (nested):**
```
function process(order) {
  if (order != null) {
    if (order.items.length > 0) {
      if (order.customer.isActive) {
        // actual logic buried at level 3
      }
    }
  }
}
```

**After (guard clauses):**
```
function process(order) {
  if (order == null) return;
  if (order.items.length == 0) return;
  if (!order.customer.isActive) return;

  // actual logic at base level
}
```

Benefits:
- Main logic not buried
- Each precondition explicit
- Adding conditions doesn't increase nesting
- Happy path clearly visible

---

## Explanatory Variables

Replace complex expressions with named intermediates.

**Before:**
```
if (user.age >= 18 && user.country == "US" && user.hasVerifiedEmail) {
```

**After:**
```
isAdult = user.age >= 18;
isInSupportedRegion = user.country == "US";
hasCompletedVerification = user.hasVerifiedEmail;

if (isAdult && isInSupportedRegion && hasCompletedVerification) {
```

---

## Named Constants

Replace magic values.

**Before:**
```
if (response.status == 404) {
  sleep(86400000);
```

**After:**
```
NOT_FOUND = 404;
ONE_DAY_MS = 24 * 60 * 60 * 1000;

if (response.status == NOT_FOUND) {
  sleep(ONE_DAY_MS);
```

---

## Positive Conditionals

Negative conditions require extra mental processing.

- Prefer `if (isValid)` over `if (!isInvalid)`
- Prefer `if (hasPermission)` over `if (!isRestricted)`

---

## Symmetry

Express the same idea the same way everywhere.

- If one case uses guard clause, similar cases should too
- If one converter is `toJSON`, others are `toXML`, `toCSV`—not `convertToXML`

---

## Nesting Rule

If nesting exceeds 3 levels:
1. Extract nested logic to well-named function
2. Use guard clauses for edge cases
3. Decompose conditions into named booleans
