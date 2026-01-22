# Naming

Names are the single most impactful readability factor. Good names eliminate comments and reduce cognitive load.

---

## Core Principle

Every name should answer: Why does this exist? What does it do? How is it used?

If a name needs a comment to explain it, the name has failed.

---

## Conventions

| Element | Part of Speech | Examples |
|---------|----------------|----------|
| Variables, Classes | Nouns | `customer`, `orderProcessor`, `shippingAddress` |
| Functions, Methods | Verbs | `calculateTotal`, `fetchUserData`, `validateInput` |
| Booleans | Questions | `isValid`, `hasPermission`, `canExecute` |

---

## Guidelines

**Reveal intent, not implementation**
- Yes: `daysSinceLastModification`
- No: `d`, `days`, `elapsedTime`

**Match length to scope**
- Loop index `i` is fine for 3 lines
- Long-lived names need description

**Use domain language**
- If experts say "invoice", don't call it `billingDocument`
- Reduces translation overhead

**Be consistent**
- Pick one word per concept: `fetch` everywhere
- Don't mix `fetch`, `get`, `retrieve`, `load`

**Be specific, not generic**
- No: `data`, `info`, `temp`, `result`, `manager`, `processor`
- Yes: `customerRecord`, `orderDetails`, `cachedResponse`, `validationResult`

---

## Avoid

| Pattern | Problem |
|---------|---------|
| Abbreviations | `custAddr` harder than `customerAddress` |
| Hungarian notation | `strName`, `intCount` — IDEs show types |
| Single letters | Except `i`/`j` for indices, `e` for exceptions |
| Numbered names | `data1`, `data2` — need meaningful differences |
| Disinformation | `accountList` when it's a Set |
