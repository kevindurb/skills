# Functions

Functions are the unit of readability. Keep them small and focused.

---

## Size

| Lines | Status |
|-------|--------|
| 5-20 | Ideal |
| 20-50 | Warning—consider splitting |
| >50 | Split immediately |

If you can't see the whole function without scrolling, it's too long.

---

## Single Responsibility

A function should:
- Do one thing
- Operate at one level of abstraction
- Be describable in a simple sentence

**Mixed abstraction (bad):**
```
function processOrder(order) {
  validateOrder(order);              // high-level

  connection = db.getConnection();   // suddenly low-level
  stmt = connection.prepare("INSERT INTO orders...");
  stmt.execute(order.id, order.total);
  connection.close();

  sendConfirmationEmail(order);      // back to high-level
}
```

**Consistent abstraction (good):**
```
function processOrder(order) {
  validateOrder(order);
  saveOrder(order);
  sendConfirmationEmail(order);
}
```

---

## Arguments

| Count | Guidance |
|-------|----------|
| 0 | Ideal for queries |
| 1 | Common and clear |
| 2 | Readers must understand relationship |
| 3+ | Use options object or create class |

---

## Command-Query Separation

Functions should either:
- **Do something** (command) — modify state, return nothing
- **Return something** (query) — answer question, no side effects

Not both.

---

## No Hidden Side Effects

Side effects make code unpredictable:
- Modifying global state
- Changing input parameters
- Making undocumented external calls

If a function has side effects, make them obvious from the name.
