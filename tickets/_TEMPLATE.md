---
id: T-YYYYMMDD-NN
title: <short imperative title, ≤80 chars>
status: BACKLOG
priority: P2
module: core
type: FEATURE
phase: N/A
created: YYYY-MM-DD
last_touched: YYYY-MM-DD
plan_id: null
journal_entries: []
blocked_by: []
related: []
---

# T-YYYYMMDD-NN — <Title>

## Problem / Opportunity

<One paragraph. Why does this ticket exist? What is the gap, bug, opportunity, or architectural requirement? Be specific about observed symptoms or the target capability.>

## Acceptance Criteria

<Measurable checklist. Each item must be verifiable without subjective ambiguity. A ticket cannot move to DONE until every criterion is satisfied.>

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Open Questions

<Bullet list. Resolve open questions before moving status to IN_PROGRESS. Move answered questions to the Decision Log.>

- Q1: <question>
- Q2: <question>

## Notes Log

<Append-only. Every turn or work session adds a new entry at the BOTTOM. Never overwrite prior entries.>

### YYYY-MM-DD HH:MM <TZ> — <Model> (<session-label>)
<Initial entry: what triggered opening this ticket, initial findings, context.>

## Decision Log

<Append-only. Each entry records an architectural choice, scope decision, or resolved question.>

- YYYY-MM-DD: <decision>. <Brief rationale.> <Source: user / audit / spec / experiment.>

## Resolution

<Filled when status moves to DONE. Lists the closing journal entry, relevant commit IDs or pull requests, and a concise summary of the shipped outcome.>

<!--
=============================================================================
FIELD REFERENCE — remove or retain as comments for guidance:
=============================================================================

status: BACKLOG | READY | IN_PROGRESS | IN_PLAN | BLOCKED | DONE | ABANDONED | OBSOLETE | SUPERSEDED
priority: P0 (urgent/blocker) | P1 (high) | P2 (medium) | P3 (low)
type: PROTOTYPE | HARDENING | FEATURE | BUG | REFACTOR | DRIFT | SPIKE | OPS

  PROTOTYPE    = Phase 1 — rapid implementation to validate feasibility and behavior
  HARDENING    = Phase 2 — comprehensive testing, edge cases, benchmarks, error handling
  FEATURE      = new system capability
  BUG          = unexpected defect, regression, or crash in existing code
  REFACTOR     = code structural improvement without behavioral change
  DRIFT        = documented contract/spec disagrees with actual codebase implementation
  SPIKE        = time-boxed research, evaluation, or proof-of-concept
  OPS          = tooling, workflow automation, CI/CD, dependencies

phase: 1 | 2 | N/A
  1   = Phase 1 (PROTOTYPE / SPIKE)
  2   = Phase 2 (HARDENING / PRODUCTIONIZATION)
  N/A = Bug fixes, governance, tooling, refactors

plan_id: SHORT_UPPERCASE_SLUG of the governing plan, or null
journal_entries: List of journal filenames (without path) in ai_system/ai_journal/
blocked_by: List of T-IDs that must be DONE before this ticket can proceed
related: Associated tickets for contextual reference

=============================================================================
EXTRA SECTIONS FOR `type: PROTOTYPE` TICKETS (Optional Iterative Discipline)
=============================================================================

## Thesis
<What capability or design hypothesis does this prototype test?>

## Shortcuts Taken
<Append technical debt, temporary stubs, hardcoded configs, or skipped test coverage.
This list becomes the scope for the subsequent HARDENING ticket.>
- [ ] <shortcut> — <what the production version requires>

## Findings & Verdict
<PROMOTE (proceed to hardening) | ITERATE (refine prototype) | DISCARD (hypothesis rejected)>
-->
