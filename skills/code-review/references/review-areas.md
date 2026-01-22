# Review Areas Reference

Detailed checklists for each review priority area.

---

## 1. Correctness & Logic

**Trace execution paths:**
- What value does each variable hold at each point?
- Under what conditions does execution reach each line?
- Are loop termination conditions correct for first and last elements?

**Edge cases to verify:**
- [ ] Empty/null inputs
- [ ] Single-element cases
- [ ] Min/max boundary values
- [ ] Negative values when positive expected
- [ ] Very large inputs (overflow potential)
- [ ] Unicode/special characters

**Boolean logic:**
- [ ] All `<`, `<=`, `>`, `>=` operators correct
- [ ] Complex boolean expressions have explicit parentheses
- [ ] No accidental assignment (`=` vs `==`)
- [ ] Null checks ordered before member access

---

## 2. Performance

**Algorithm complexity:**
- [ ] No unnecessary nested loops (O(n²) or worse)
- [ ] List.contains() in loops → use Set for O(1)
- [ ] String concatenation in loops → use StringBuilder
- [ ] Appropriate data structures for access patterns

**Database:**
- [ ] No N+1 query patterns
- [ ] Indexes exist for WHERE, JOIN, ORDER BY columns
- [ ] No SELECT * when specific columns suffice
- [ ] Eager loading used where appropriate

**Resources:**
- [ ] All opened resources are closed (connections, files, streams)
- [ ] Close happens even on exception paths (try-with-resources)
- [ ] No unbounded caches or collections

**Caching:**
- [ ] Expensive operations cached appropriately
- [ ] Cache invalidation strategy clear
- [ ] No cache stampede potential

---

## 3. Architecture

**SOLID principles:**
- [ ] Single Responsibility: Can describe class purpose without "and"?
- [ ] Open/Closed: No long if/else or switch on types?
- [ ] Liskov: No required casting after using base type?
- [ ] Interface Segregation: No empty method implementations?
- [ ] Dependency Inversion: Dependencies injected, not created?

**Layer boundaries:**
- [ ] No business logic in presentation layer
- [ ] No database queries in controllers
- [ ] No UI framework dependencies in domain services

**Design patterns:**
- [ ] Patterns used solve actual problems
- [ ] No premature abstraction
- [ ] No god objects or singletons hiding dependencies

---

## 4. Error Handling

**Anti-patterns to flag:**
- [ ] Empty catch blocks (swallowing exceptions)
- [ ] Catch-all generic Exception without re-throw
- [ ] Log-and-throw (duplicate stack traces)
- [ ] Generic exceptions without specific error info

**Retry patterns:**
- [ ] Exponential backoff for transient failures
- [ ] Maximum retry limits set
- [ ] Non-retryable errors identified (4xx vs 5xx)

**Circuit breakers:**
- [ ] Failure thresholds configured
- [ ] Fallback behavior defined
- [ ] Recovery/half-open state handled

---

## 5. Testing

**Coverage:**
- [ ] New code paths have tests
- [ ] Critical paths (auth, payments) near 100%
- [ ] Edge cases covered
- [ ] Error paths tested

**Quality:**
- [ ] Tests have meaningful assertions (not just "no exception")
- [ ] Test names describe behavior being verified
- [ ] Tests are isolated and independent
- [ ] No flaky tests (timing, shared state, order dependency)

**Mocking:**
- [ ] External services mocked at boundaries
- [ ] Own database not over-mocked in integration tests
- [ ] Mock complexity reasonable

---

## 6. Concurrency

**Race conditions:**
- [ ] No check-then-act patterns without synchronization
- [ ] Compound operations are atomic
- [ ] Shared mutable state protected

**Deadlock prevention:**
- [ ] Consistent lock ordering
- [ ] No external calls while holding locks
- [ ] Timeout on lock acquisition where appropriate

**Async patterns:**
- [ ] No `async void` (C#) — return Task
- [ ] No blocking on async with .Result/.Wait()
- [ ] All promises have error handling

---

## 7. API Design

**REST conventions:**
- [ ] Nouns for resources, not verbs
- [ ] Appropriate HTTP methods (GET retrieves, POST creates, etc.)
- [ ] Correct status codes (201 Created, 204 No Content, etc.)
- [ ] Consistent error response format

**Versioning:**
- [ ] Breaking changes require new version
- [ ] Non-breaking: adding optional fields, new endpoints
- [ ] Breaking: removing/renaming fields, changing types

---

## 8. Data Handling

**Transactions:**
- [ ] Clear transaction boundaries
- [ ] Appropriate isolation level
- [ ] Error handling commits/rolls back correctly

**Migrations:**
- [ ] Rollback script exists and tested
- [ ] Large operations batched
- [ ] Backwards compatible during deploy window

---

## 9. Dependencies

**Security:**
- [ ] No known vulnerabilities in new dependencies
- [ ] Lock file updated and committed
- [ ] License compatible with project

**Hygiene:**
- [ ] Dependency actually needed
- [ ] Not duplicating existing functionality
- [ ] Maintained and actively supported
