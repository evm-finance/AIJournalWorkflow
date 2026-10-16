# AGENTS.md — Multi-Agent Engineering & Governance Protocol

> **You are an AI agent collaborating in a multi-model, multi-session development environment.**  
> Uncertainty expressed protects system integrity; confidence performed creates silent degradation.  
> Identify your model family and turn intent in every state header and journal entry.

---

## 1. Context Preservation & Core Philosophy

This repository is governed by the **AI Journal Workflow framework**. AI models lose memory between distinct chat sessions, context compactions, and tool boundaries. To maintain institutional continuity and architectural discipline:

1. **Working State is Explicit**: Immediate turn focus lives in [`ACTIVE_STATE.md`](ACTIVE_STATE.md) (L1 Cache).
2. **Intent & Tasks are Structured**: Backlog, acceptance criteria, and decision histories live in [`tickets/`](tickets/) (L2 Working Memory).
3. **History is Immutable**: All completed changes and rationale are recorded append-only in [`ai_system/ai_journal/`](ai_system/ai_journal/) (L3 Immutable Ledger).
4. **Specification Outranks Memory**: Never implement from sampled keywords, partial recall, or ephemeral chat assumptions. Specifications and tickets must be read in full.

---

## 2. Doc Hierarchy & Source of Truth

Authority flows strictly from top to bottom. If a lower-level document contradicts a higher-level document, the lower-level artifact is stale and must be flagged as `type: DRIFT`:

```text
0. System Architectural Specifications & Invariants  (SUPREME for architecture)
1. AGENTS.md                                         (SUPREME for process & governance)
2. tickets/                                          (Authoritative for requirements & tasks)
3. Multi-phase Plans (PLAN.md)                       (Authoritative for scheduled step order)
4. ACTIVE_STATE.md                                   (Current turn focus & blocker state)
5. ai_system/ai_journal/                             (Immutable audit log of all prior work)
6. Source Code & Configuration Files                 (Implementation)
```

---

## 3. Priority Hierarchy — What to Fix First

When multiple problems or tickets compete, the higher tier wins regardless of novelty or perceived ease:

| Tier | Focus | Central Question | Consequence of Failure |
|---|---|---|---|
| **H1** | **System & Data Integrity** | *Can this corrupt state, break migrations, or compromise secrets?* | Catastrophic failure; unrecoverable loss. |
| **H2** | **Core Architecture & Invariants** | *Are interface contracts, data flows, and state boundaries intact?* | System flies blind; logic disconnects. |
| **H3** | **Execution Correctness** | *Do methods execute, fail gracefully, and handle edge cases?* | Silent logic defects and regressions. |
| **H4** | **Features & Optimizations** | *Is the new capability built, and is performance optimized?* | Suboptimal, but honest and verifiable. |
| **H5** | **Observability, Docs & Cleanup** | *Are logs, telemetry, and documentation clear and accurate?* | Slower human/agent diagnosis. |

> **The Invalidation Invariant:**  
> A defect at a higher tier invalidates measurements and benchmarks taken at any tier below it. Never evaluate feature performance (H4) while core data contracts or error pipelines (H2/H3) are broken.

---

## 4. Two-Phase Development Model

All substantial development proceeds through two distinct phases to maximize token budget efficiency and ensure verifiable results:

| Dimension | Phase 1 — PROTOTYPE / SPIKE | Phase 2 — HARDENING / PRODUCTION |
|---|---|---|
| **Objective** | *Does this approach solve the core problem?* | *Is this implementation robust, tested, and maintainable?* |
| **Validated By** | Minimal end-to-end execution, sanity checks | Comprehensive test suites, edge case handling, benchmarks |
| **Licence** | Rapid discovery; stubbing edge cases, local constants | Rigor; zero hardcodes, strict typing, clean error handling |
| **Testing Rule** | **Do not write exhaustive unit tests in Phase 1.** (Saves token budget until design is proven). | **Writing tests is mandatory in Phase 2.** |
| **Exit Bar** | Written verdict: **PROMOTE / ITERATE / DISCARD** | All shortcuts paid down, test suite green, docs updated |

### Phase 1 Discipline
- Every shortcut, stub, or deferred edge case taken during Phase 1 must be documented in the ticket under `## Shortcuts Taken`.
- This list directly forms the backlog for the paired Phase 2 ticket.

---

## 5. State Header

Every agent response touching code, configuration, or plans MUST begin with this header:

```text
[<MODEL_NAME>] | [Module: <module/feature>] | [Ticket: T-YYYYMMDD-NN | none]
[Phase: 1 PROTOTYPE | 2 HARDENING | N/A — <reason>]
[Tier: H1 integrity | H2 architecture | H3 execution | H4 feature | H5 observability]
[System State: Clear | Uncertain — need to read <X> | Tension — conflicts with <Y>]
[Invariants Checked: <which critical constraints were verified this turn>]
```

**Rule**: If `System State` is not `Clear`, resolve uncertainties and read the required specifications before modifying code.

---

## 6. Process — Tickets, Plans & Journaling

### Tickets (`tickets/`)
- Every non-trivial feature, bug, refactor, or architectural drift belongs in a dedicated ticket: `tickets/T-YYYYMMDD-NN-<slug>.md`.
- Copy [`tickets/_TEMPLATE.md`](tickets/_TEMPLATE.md) to initialize.
- Front-matter status transitions (`BACKLOG`, `READY`, `IN_PROGRESS`, `BLOCKED`, `DONE`, `ABANDONED`) must be updated in [`tickets/INDEX.md`](tickets/INDEX.md) in the same turn.
- The `## Notes Log` is **append-only**. Never overwrite prior session notes.
- Resolved design questions are appended to the `## Decision Log`.
- When closed, tickets move to [`tickets/archive/`](tickets/archive/).

### Journaling (`ai_system/ai_journal/`)
- **Journaling is non-negotiable.** Every session modifying files must produce an entry in `ai_system/ai_journal/YYYY-MM-DD_<slug>.md`.
- Capture: Intent, actions taken, files changed, files explicitly left untouched, and verification command results.
- **Preserve Before Overwrite:** Before substantially revising any load-bearing architecture doc or governance rule, paste the prior content verbatim into a journal entry. Git preserves lines; the journal preserves *human and agent reasoning*.

---

## 7. Absolute Prohibitions

1. **No Unlogged Changes:** Never modify source code without recording the change in an active ticket and session journal.
2. **No False Attribution:** Accurately identify your model family and role in state headers and journal entries.
3. **No Acting on Sampled Specs:** Grepping an architectural specification for a keyword is not reading. Read the document cover-to-cover to understand overriding clauses and context.
4. **No Hidden Drift:** When code and documentation diverge, document it immediately as a `type: DRIFT` ticket.
5. **No Backup Destruction:** Always preserve baseline documents in the journal before sweeping overwrites.
6. **No Phase Mixing:** Do not spend tokens writing extensive test suites in Phase 1 prototypes; do not ship unverified Phase 1 stubs without Phase 2 hardening.
7. **No Bypassing Verification Gates:** Never mark a ticket or plan step `DONE` without executing the automated verification suite.

---

## 8. Verification & Completion Gate

Before marking any ticket or plan phase `DONE`:

1. **Build / Typecheck**: Verify that the project compiles with zero type errors.
2. **Test Suite**: Run the automated test runner; confirm all tests pass.
3. **Linter / Formatting**: Verify code matches style conventions with zero warnings.
4. **Cold Audit Checklist**:
   - [ ] All Acceptance Criteria in the ticket verified.
   - [ ] No unlisted shortcuts or orphaned stubs remain.
   - [ ] Resolution section filled in ticket.
   - [ ] Ticket moved to `tickets/archive/` and `tickets/INDEX.md` updated.
   - [ ] Closing session journal written in `ai_system/ai_journal/`.
