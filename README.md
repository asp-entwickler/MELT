# M.E.L.T.

**Model → Execute → Log → Trim**

> Documentation that maintains itself, written by the system that has to obey it.

MELT is based on a simple observation:

Large projects do not fail because the AI cannot generate code.

They fail because architectural intent slowly evaporates across sessions, prompts, refactors, contributors, and time.

You do not lose system understanding all at once.

You lose it in fragments:
- why this invariant exists
- why this endpoint behaves strangely
- why this migration was done this way
- why this "temporary" workaround became infrastructure
- why this decision must not be reversed six months later

MELT treats architectural memory as a first-class engineering artifact.

Not documentation theater.
Not endless ADR collections.
Not AI hype.

Just durable operational memory for humans and agents.

---

# Setup

1. Put `AGENTS.md` in your project folder
2. Create identical copy of `AGENTS.md` with name `CLAUDE.md`
3. Put `DECISIONS.md` in your project folder
4. Create empty `CHANGELOG.md`
5. Create:
   - `docs/concepts/`
   - `docs/implemented/`
6. Open the repository in Claude Code / Codex / Cursor
7. Run the initialization prompt below

---

# Initialization prompt

```text
Read AGENTS.md and analyze the current repository structure, architecture, conventions, and implementation patterns.

Then:

1. Populate DECISIONS.md with the real architectural invariants, constraints, conventions, and cross-module rules already present in the system.
2. Remove placeholder sections that are not relevant.
3. Keep only durable decisions with long-term architectural value.
4. Do not invent abstractions, layers, or processes that do not already exist.
5. Prefer operational reality over idealized architecture.
6. Keep DECISIONS.md compact and maintainable.
7. If uncertain whether something is a durable invariant — omit it.

The goal is not to document everything.

The goal is to create durable architectural memory that future agent sessions can reliably obey.
```

---

# Core idea

MELT separates:
- temporary implementation reasoning
from
- durable architectural intent

The temporary reasoning melts away.

The distilled system knowledge remains.

---

# Repository structure

```text
AGENTS.md / CLAUDE.md
DECISIONS.md
CHANGELOG.md
docs/
```

## AGENTS.md / CLAUDE.md

Operational contract for the coding agent.

Defines:
- how the agent should behave
- when to stop
- when to check architectural constraints
- how to maintain changelog and decisions

This is not architecture documentation.

It is agent operating procedure.

---

## DECISIONS.md

Durable architectural memory.

Contains:
- invariants
- cross-module constraints
- semantic rules
- integration assumptions
- things future sessions must not silently break

This is intentionally compact.

Only information with long-term architectural value belongs here.

---

## CHANGELOG.md

Temporary implementation trail.

During development it may contain:
- noisy iterations
- partial attempts
- reasoning residue
- implementation notes

At the end of a feature or session, the user may ask the agent to compress it into:
- implemented functionality
- meaningful system changes
- durable feature-level history

Signal remains.

Noise melts away.

---

## docs/concepts/

Temporary feature specifications and implementation scaffolding.

Most concept documents are expected to disappear after implementation.

---

## docs/implemented/

Concepts stable enough to survive implementation and become long-term system knowledge.

---

# Philosophy

MELT is intentionally minimal.

The goal is not more process.

The goal is reducing architectural entropy in long-running AI-assisted development.

Documentation stops being something humans write and nobody reads.

It becomes durable memory shared between humans and agents.

---

# Status

Experimental.

Built from real-world usage in production systems with coding agents.
