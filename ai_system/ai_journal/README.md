# AI Journal (`ai_journal`)

This directory is the immutable historical ledger of all development sessions, architectural decisions, and code modifications performed across the repository.

## Operational Rules

1. **Append-Only / Immutable**: Never edit, rewrite, or delete prior journal entries. If a past conclusion was mistaken or superseded, create a new dated journal entry explaining what was learned and why the direction changed.
2. **File Naming Convention**:
   `YYYY-MM-DD_<descriptive-slug>.md`
   Example: `2026-10-15_websocket_reconnection_backoff.md`
   If multiple distinct entries occur on the same day, use distinct slugs or suffix sequence numbers (`_02_...`).
3. **Trigger**:
   - Complete work on any ticket or plan step.
   - Significant architectural decisions or pivots.
   - Preserving verbatim text before modifying load-bearing governance or specification documents.
4. **Template**:
   Copy [`_TEMPLATE.md`](_TEMPLATE.md) when writing a new entry.

---

## Required Structure

Each journal entry should capture:
- **Metadata Header**: Date, descriptive title, AI model family/agent identifier, linked ticket ID, and scope.
- **Intent**: The specific motivation, problem statement, or directive prompting the change.
- **Actions Taken**: Clear breakdown of what was created, modified, or deleted.
- **Scope Boundaries**: Explicit note of files/modules intentionally left untouched to prevent scope creep.
- **Verification Gates**: Commands executed (build, test, lint, typecheck) and their actual outputs/pass rates.
- **Handoff / Next Steps**: Guidance for the subsequent agent or human operator.
