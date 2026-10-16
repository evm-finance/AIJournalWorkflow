# Tickets System

This directory is the persistent task backlog, design log, and decision tracker for the project. It bridges abstract intent (conversations, brainstorms, user directives) with concrete execution (`PLAN.md` phases, code changes, and journal entries).

Authoritative governance rules live in [`../AGENTS.md`](../AGENTS.md).

---

## What goes here

| You want to capture... | Action |
|---|---|
| "Wouldn't it be nice if..." / "We should eventually..." | New ticket, status `BACKLOG` |
| Concrete problem with acceptance criteria sharp enough to implement | Same ticket $\rightarrow$ status `READY` |
| Multi-step implementation plan for an active ticket | `PLAN.md` linking `SOURCE_TICKETS` |
| Live train-of-thought, design iterations, or intermediate findings during a session | Notes Log of the active ticket |
| Architecture consensus or resolution of an open question | Decision Log of the active ticket |
| A change you just made to code or configuration | Journal entry in `ai_system/ai_journal/`, linking the ticket header `[Ticket: T-…]` |
| A discrepancy ("code contradicts specification at X") | New ticket, `type: DRIFT`, status `BACKLOG` or `READY` |
| A bug ("system crashes or misbehaves under Y") | New ticket, `type: BUG`, status `READY` (P0 if production blocker) |

## What does NOT go here

- **Immutable historical record of changes** $\rightarrow$ That belongs in [`../ai_system/ai_journal/`](../ai_system/ai_journal/).
- **Ephemeral scratchpads / immediate turn state** $\rightarrow$ That belongs in [`../ACTIVE_STATE.md`](../ACTIVE_STATE.md).
- **Core project architecture specification** $\rightarrow$ That belongs in system architecture documents / specs.

---

## Directory contents

| File / folder | Purpose |
|---|---|
| `README.md` | This operational primer |
| `INDEX.md` | Curated index of **active** tickets grouped by priority (`P0`–`P3`) and status |
| `archive/` | Terminal tickets (`DONE`, `OBSOLETE`, `SUPERSEDED`, `ABANDONED`) |
| `_TEMPLATE.md` | Master template to copy when creating any new ticket |
| `T-YYYYMMDD-NN-<slug>.md` | Individual ticket files for active work |

---

## Ticket IDs

Format: `T-YYYYMMDD-NN`
- `YYYYMMDD`: Calendar date the ticket was opened.
- `NN`: Two-digit daily sequence counter (`01`, `02`, ...).

The Ticket ID never changes once assigned. If the scope or title evolves, update the filename slug or ticket title, but retain the numeric ID to preserve link integrity across git history and journals.

---

## Lifecycle

```text
        opened
          │
          ▼
       BACKLOG ────── pruned ──────► ABANDONED
          │
          │ (acceptance criteria refined)
          ▼
        READY
          │
          │ (work begins / covered by PLAN.md)
          ▼
     IN_PROGRESS / IN_PLAN ─── blocked by dep ──► BLOCKED
          │                                         │
          │ (all criteria verified + journaled)     │ (dep cleared)
          ▼                                         │
        DONE ◄──────────────────────────────────────┘
```

Status is authoritatively declared in YAML front-matter. **Active** tickets reside in `tickets/`; **closed** tickets move to `tickets/archive/` (the folder move is for navigation and file hygiene; the front-matter status remains authoritative).

---

## Archive

When a ticket reaches a terminal status, move its file to `tickets/archive/` and update `INDEX.md` in the same turn:

| Status | When to archive |
|---|---|
| `DONE` | All Acceptance Criteria ticked, Resolution section filled, closing journal linked |
| `OBSOLETE` | Architectural direction changed; scope is no longer applicable |
| `SUPERSEDED` | Replaced by a newer ticket (state `superseded_by: T-...` in front-matter) |
| `ABANDONED` | Pruned from backlog with documented rationale in the Notes Log |

Ticket IDs and filenames are never altered upon archiving.

---

## Opening a new ticket

1. Identify the next sequence number `NN` for today's date by checking `INDEX.md` or listing `tickets/T-<today>-*.md`.
2. Copy `_TEMPLATE.md` to `tickets/T-<today>-NN-<short-slug>.md`.
3. Fill in the YAML front-matter (all required fields; use `null` or `[]` if empty).
4. Write the **Problem / Opportunity** statement.
5. Add the initial entry to **Notes Log**: timestamp, model identification, session context, and trigger.
6. Add an entry to `INDEX.md` under the appropriate priority section.
7. Record the ticket creation in your session journal in `ai_system/ai_journal/`.

---

## Working an existing ticket

1. Read the ticket's complete **Notes Log** and **Decision Log** to restore context before taking action.
2. Add a new dated entry at the **bottom** of the Notes Log (append-only).
3. Execute the implementation changes.
4. Update `last_touched` in the front-matter.
5. If status, priority, or blockers change, update `INDEX.md` in the same turn.
6. Record any resolved architectural choices in the **Decision Log**.
7. Write a session journal in `ai_system/ai_journal/` referencing the ticket ID.

---

## Closing a ticket

A ticket is marked `status: DONE` when:
- Every Acceptance Criterion checkbox is verified and marked `[x]`.
- The closing journal entry is written and listed under `journal_entries:` in front-matter.
- The `## Resolution` section summarizes the final changes and outcome.
- The ticket file is moved to `tickets/archive/` and removed from active tables in `INDEX.md`.
