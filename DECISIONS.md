# [Project Name] — Business Decisions & Invariants

This file is the durable architectural memory of the system.

The coding agent reads this before every change to:
- detect conflicts
- preserve invariants
- avoid reintroducing previously rejected patterns
- reduce architectural drift across sessions

---

## CROSS-MODULE: API Conventions

### Request / response naming (invariant)

- Define naming conventions here (snake_case, PascalCase, etc.)
- Define serialization mapping approach
- All new DTOs must follow the convention without exception

### Time handling (invariant)

- All UTC timestamps use `timestamp with time zone` (`timestamptz`) — never `timestamp`
- Never use `DateTime.Now`, `DateTimeOffset.Now`, or implicit system timezone APIs
- Use `IClock` abstraction for current time
- Use IANA timezone database for timezone conversion

---

## MODULE: [Auth / Access Control]

### Access model

- [Define access rules]
- [Define expiration semantics]
- [Define access validation points]

### Session model

- [Cookie / JWT / other]
- Store only hashed session keys
- All auth timestamps are UTC

### Endpoint separation (invariant)

- Internal and public endpoints must remain separate
- Internal endpoints must never become public accidentally

---

## MODULE: [Billing / Subscriptions]

### Billing rules

- [Provider and integration details]
- [Webhook ordering rules]
- [Access extension rules]

### Permission & access rules

- [Role model / permission boundaries]
- [User vs admin capabilities]
- [Cross-module access constraints]

---

## MODULE: [Domain Entity with complex semantics]

### Semantics

- [Define intent vs calculated values]
- [Optional vs required fields]
- [Meaning of missing values]

### Invariants

- [Constraint 1]
- [Constraint 2]

---

## MODULE: [AI / External API]

### Context / payload rules

- [What is sent]
- [Size constraints]
- [What must not be added before refactor]

### Tolerance / thresholds

- [Matching thresholds]
- Do not change thresholds without explicit decision

### Versioning

- [Prompt / config versioning rules]
- Older versioned prompts must remain immutable

---

## MODULE: [Pipeline / Queue / Infrastructure]

### Handler rules

- [Stateless vs stateful]
- [Execution ordering]
- [Rate limiting]

### Queue model

- [Queue type]
- [Serial vs parallel processing]

---

## MODULE: [Database & Migrations]

### Database rules

- No business logic in the database
- Constraints are allowed
- Every migration must include corresponding entity/mapping updates
- All FK constraints and indexes are added explicitly

### Migration naming

Use:
`YYYYMMDDNN_Description`

---

## Additional context

### docs/concepts/

Temporary specifications.
May change rapidly.
May disappear after implementation.

### docs/implemented/

Implemented concepts stable enough for future reference.
