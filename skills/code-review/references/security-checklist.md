# Security Review Checklist

OWASP-aligned checklist for security-focused code review.

---

## Input Validation

- [ ] Server-side validation present (client-side is UX only)
- [ ] Allowlist validation, not blocklist
- [ ] Parameterized queries for all database operations
- [ ] No string concatenation in SQL/commands
- [ ] File uploads: type validation, size limits, safe storage location

**Injection patterns to search for:**
```
"SELECT.*\+.*"     # SQL concatenation
"os.system\("      # Command injection
"subprocess.*shell=True"
"eval\(|exec\("    # Code injection
```

---

## Authentication & Sessions

- [ ] Strong password hashing (bcrypt, Argon2 — not MD5/SHA1)
- [ ] Session tokens: ≥128 bits entropy
- [ ] Cookie attributes: `HttpOnly`, `Secure`, `SameSite=Strict`
- [ ] Session regeneration after login
- [ ] Complete session invalidation on logout

**JWT-specific:**
- [ ] "none" algorithm explicitly rejected
- [ ] Algorithm specified server-side, not from token
- [ ] `exp`, `aud`, `iss` claims validated
- [ ] Secrets ≥256 bits of cryptographic randomness

---

## Authorization

- [ ] Default deny policy
- [ ] All authorization checks server-side
- [ ] IDOR prevention (can user A access user B's resources?)
- [ ] Privilege escalation paths reviewed
- [ ] Admin functions protected

---

## Secrets Management

- [ ] No hardcoded secrets, API keys, passwords
- [ ] No secrets in logs or error messages
- [ ] Secrets loaded from environment/vault, not config files
- [ ] `.gitignore` includes secret files

**Patterns to search for:**
```
password\s*=\s*["']
api_key\s*=\s*["']
secret\s*=\s*["']
AWS_SECRET
-----BEGIN.*PRIVATE
```

---

## Cross-Site Scripting (XSS)

- [ ] Output encoding appropriate to context (HTML/JS/URL)
- [ ] Framework auto-escaping enabled

**Dangerous escape hatches (flag for review):**
- React: `dangerouslySetInnerHTML`
- Angular: `bypassSecurityTrust*`
- Vue: `v-html`

---

## Cryptography

- [ ] Modern algorithms: AES-256, RSA-2048+, ECDSA P-256+
- [ ] Cryptographically secure random number generation
- [ ] No custom crypto implementations
- [ ] Proper key management and rotation

---

## Error Handling

- [ ] No sensitive information in error responses
- [ ] No stack traces exposed to users
- [ ] Security events logged appropriately
- [ ] Failed authentication attempts rate-limited
