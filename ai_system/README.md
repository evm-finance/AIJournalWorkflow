# AI System Architecture (`ai_system`)

This directory houses the persistent knowledge, cognitive memory, and historical journal systems that enable multi-agent collaboration across independent AI tools (Antigravity, Cursor, Claude Code, subagents).

## The Context Preservation Problem

AI coding assistants are stateless across fresh sessions and context window compactions. Without an explicit, out-of-band memory architecture:
1. **Context Train Loss**: Rationale, rejected alternatives, and architectural trade-offs vanish when a chat thread ends or overflows.
2. **Multi-Agent Drift**: Multiple agents operating in parallel or sequence clobber each other's assumptions or make contradictory changes.
3. **Ghost Invariants**: Subtle constraints known only through conversation get violated during subsequent refactors.

## Memory Layer Architecture

The system employs a three-tier memory model:

```text
┌─────────────────────────────────────────────────────────────┐
│ Tier 1: ACTIVE_STATE.md (L1 Cache — Ephemeral & Mutable)   │
│ Single-writer, continuously overwritten present state.     │
│ Immediate turn goal, active ticket, blockers, next steps.   │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ Tier 2: tickets/ (L2 Structured Working Memory)             │
│ Long-lived task backlog, acceptance criteria, notes log,   │
│ decision logs, and resolution tracking.                     │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ Tier 3: ai_system/ai_journal/ (L3 Immutable Ledger)         │
│ Append-only dated records (YYYY-MM-DD_<slug>.md).           │
│ Intent, actions taken, files changed, verification gates.   │
└─────────────────────────────────────────────────────────────┘
```

## Core Invariants

1. **Immutable Historical Record**: Past journal entries in `ai_journal/` are NEVER edited, rewritten, or deleted to reflect new understanding. New understanding is documented in a new dated journal entry.
2. **Preserve Before Overwrite**: Before overwriting any load-bearing architectural doc or governance rule, capture the prior text verbatim in a journal entry. Git captures code diffs; the journal captures *human and agent intent*.
3. **Auditability**: Every code modification must link back to an active ticket and produce a corresponding journal entry detailing intent and test verification.
