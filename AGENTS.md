# [Project Name] — Project Context for Coding Agents

## Stack

- **[Service 1]:** [e.g. C# / .NET 8, ASP.NET Core]
- **[Service 2]:** [e.g. PostgreSQL, NHibernate ORM, FluentMigrator]
- **[Frontend]:** [e.g. Vue 3 + Vite + Tailwind]
- **[AI/External]:** [e.g. OpenAI Responses API]
- **Time:** [e.g. NodaTime — always UTC in storage, IANA tz for user-local display]
- **Secrets:** environment variables only — never in config files

## Project layout

```text
ServiceA/               — [description]
Project.Application/    — Application services, commands
Project.Domain/         — Entities
Project.Persistence/    — ORM mappings, migrations
Project.Api/            — Backend API
Project.Client/         — Frontend
Docs/                   — Architecture docs and concept files
```

## Key reference docs

Read these before touching the relevant module:

- `Docs/Architecture.md` — [system overview]
- `Docs/auth_concept.md` — [auth model]
- `DECISIONS.md` — business invariants, cross-module rules

---

## Core principle

The repository contains durable architectural memory.

Implementation prompts are temporary.
`DECISIONS.md` is persistent.

Do not silently reinterpret or bypass existing decisions.

The purpose of `DECISIONS.md` is preventing architectural drift across sessions and agents.

If the prompt conflicts with an existing decision:
- stop
- explain the conflict
- ask for explicit override

`DECISIONS.md` has higher priority than implementation prompts unless the user explicitly overrides the decision.

---

## Pre-change check (REQUIRED)

Before modifying any code, you must:

1. Read `DECISIONS.md`
2. Identify which module(s) the change touches
3. Check whether the requested change conflicts with existing decisions
4. If a conflict exists — stop and report it before writing code

Skip this check only if the user explicitly says so.

---

## Post-change DECISIONS update (REQUIRED)

After completing any code change, evaluate whether `DECISIONS.md` needs updating.

Update `DECISIONS.md` if the change introduces or modifies:
- business rules
- architectural constraints
- module-level invariants
- decisions future agents could conflict with

Skip `DECISIONS.md` only if nothing about the system's behavior or structure changed.

Update sections in place.
`DECISIONS.md` reflects current state — not historical evolution.

History belongs in `CHANGELOG.md`.

---

## CHANGELOG

Maintain `CHANGELOG.md` during implementation.

The changelog may temporarily contain noisy iterative reasoning, partial attempts, or implementation trail.

Do not compress, rewrite, or discard history unless explicitly requested by the user.

---

## docs/ lifecycle

`docs/concepts/`
- temporary implementation scaffolding
- active work in progress
- expected to change rapidly

`docs/implemented/`
- concepts that survived implementation
- stable enough to become system knowledge

Most concept documents are expected to disappear.

The system should retain distilled intent, not implementation noise.

---

## Code conventions

### Formatting
- Max line length: 140 characters
- [Indentation, braces style, etc.]

### Class member order
- Private fields
- Constructors
- Public properties
- Public methods
- Private methods
- Static members

### File organization
- One class per file
- Enums: [in separate files / together with the class that owns them]
- [Namespace conventions]

### Naming
- [Project-specific naming rules]

---

## Engineering rules

- [Handlers are stateless singletons — no per-request state in fields]
- [Execution order is declared in one place]
- [All timestamps are UTC; local dates use LocalDate]
- [ORM session lifecycle is managed by DI — do not open sessions manually]
- [Migrations use YYYYMMDDNN_Description naming]
