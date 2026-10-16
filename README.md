# AIJournalWorkflow

**A generalized framework for multi-agent collaboration, context preservation, and structured development governance across AI sessions.**

This repository provides an open-source, production-tested blueprint for coordinating multiple AI coding assistants (such as Google Antigravity, Cursor, Claude Code, and autonomous subagents) while eliminating context drift, hallucinated specifications, and unlogged architectural changes.

---

## The Core Concept

AI assistants are stateless across fresh sessions and context window compactions. In multi-agent or long-running development:
- **Chat context decays**: Nuanced trade-offs and rejected alternatives vanish when a chat thread ends.
- **Agents clobber each other**: Different agents working across files can contradict each other's assumptions.
- **Invariants get lost**: Without an explicit record, future prompts break subtle edge cases.

`AIJournalWorkflow` solves this by introducing a three-tiered memory and governance model directly into the git repository:

```text
┌──────────────────────────────────────────────────────────────────┐
│ Tier 1: ACTIVE_STATE.md (L1 Cache — Ephemeral & Mutable)         │
│ Single-writer, continuously overwritten present state.           │
│ Immediate turn goal, active ticket, blockers, and next steps.    │
└──────────────────────────────┬───────────────────────────────────┘
                               │
┌──────────────────────────────▼───────────────────────────────────┐
│ Tier 2: tickets/ (L2 Structured Working Memory)                  │
│ Long-lived task backlog, acceptance criteria, append-only notes  │
│ logs, decision logs, and resolution tracking.                    │
└──────────────────────────────┬───────────────────────────────────┘
                               │
┌──────────────────────────────▼───────────────────────────────────┐
│ Tier 3: ai_system/ai_journal/ (L3 Immutable Ledger)              │
│ Append-only dated records (YYYY-MM-DD_<slug>.md).                │
│ Captures intent, files changed, scope bounds, and test outcomes. │
└──────────────────────────────────────────────────────────────────┘
```

---

## Repository Structure

```text
ai_journal_workflow/
├── AGENTS.md                   # Master multi-agent governance protocol & rules
├── ACTIVE_STATE.md             # L1 immediate turn state (overwritten continuously)
├── tickets/                    # L2 task & decision management system
│   ├── README.md               # Operational guide for managing tickets
│   ├── _TEMPLATE.md            # Master ticket template (YAML front-matter + logs)
│   ├── INDEX.md                # Active tickets registry (P0/P1/P2/P3)
│   └── archive/                # Terminal tickets (DONE, OBSOLETE, SUPERSEDED)
│       └── README.md           # Archive guidelines
├── ai_system/                  # L3 AI memory & knowledge architecture
│   ├── README.md               # System overview and memory layer explanations
│   └── ai_journal/             # Immutable dated journal entries
│       ├── README.md           # Journaling guidelines and lifecycle
│       └── _TEMPLATE.md        # Session journal entry template
└── README.md                   # This document
```

---

## Key Protocols

### 1. State Header
Every agent response touching code or planning begins with a standardized State Header declaring its model, module, ticket, development phase, priority tier, and verification state:

```text
[Claude 3.7 Sonnet] | [Module: auth] | [Ticket: T-20261015-01]
[Phase: 1 PROTOTYPE | 2 HARDENING | N/A]
[Tier: H1 integrity | H2 architecture | H3 execution | H4 feature | H5 observability]
[System State: Clear | Uncertain — need to read <X>]
[Invariants Checked: Token expiration validated, session cookie secure]
```

### 2. Two-Phase Development
- **Phase 1 (PROTOTYPE / SPIKE)**: Focuses on rapid validation of hypotheses. Minimal end-to-end execution. Extensive test writing is deferred to save token budget, but all shortcuts are tracked in the ticket.
- **Phase 2 (HARDENING / PRODUCTION)**: Mandates comprehensive test coverage, edge case handling, typing, and paying down every Phase 1 shortcut before closing the ticket.

### 3. Append-Only Notes & Decisions
Tickets never overwrite history. Every agent session appends a timestamped note to the ticket's `Notes Log`, and key architectural choices are added to the `Decision Log`.

### 4. Preserve Before Overwrite
Before replacing or significantly refactoring any load-bearing architectural doc or specification, the baseline is preserved verbatim in an `ai_journal/` entry. Git tracks lines; the journal tracks reasoning.

---

## Quickstart: Adopting in Your Project

To adopt this workflow in any software project:
1. Copy `AGENTS.md` to your repository root and adjust project-specific build/test verification commands.
2. Copy `ACTIVE_STATE.md` to your root.
3. Copy the `tickets/` directory (`README.md`, `_TEMPLATE.md`, `INDEX.md`, `archive/`).
4. Copy the `ai_system/` directory (`README.md`, `ai_journal/`).
5. Instruct your AI assistants to read `AGENTS.md` before performing work.
