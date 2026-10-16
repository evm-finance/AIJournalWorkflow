# YYYY-MM-DD — <Concise Descriptive Title> (`T-YYYYMMDD-NN`)

**Model / Agent:** <e.g., Claude 3.7 Sonnet / Antigravity / Cursor / Claude Code>  
**Ticket:** <T-YYYYMMDD-NN or none>  
**Scope / Module:** <e.g., auth, api, ui, db, cross>  
**Development Phase:** <Phase 1 (PROTOTYPE) | Phase 2 (HARDENING) | N/A (fix/docs/tooling)>  

---

## 1. Intent & Scope

<What prompted this session? What bug, requirement, or directive was addressed? Why was this specific approach chosen over alternatives?>

---

## 2. Actions Taken

- **Created / Modified:**
  - `path/to/file1.ext`: <summary of change>
  - `path/to/file2.ext`: <summary of change>
- **Architectural Adjustments:**
  - <key structural or interface changes>

---

## 3. Scope Boundaries & Files NOT Changed

- Intentionally preserved existing behavior in `path/to/stable_file.ext`.
- Deferred <unrelated refactor or cleanup> to separate ticket `T-...`.

---

## 4. Verification Gate Results

Automated commands executed and their verification outcomes:

```text
# Build / Typecheck
<command> -> PASSED

# Test Suite
<command> -> PASSED (e.g., 24/24 unit tests green)

# Linter / Static Analysis
<command> -> CLEAN (0 errors, 0 warnings)
```

---

## 5. Handoff & Next Steps

- <Immediate next step for the next agent session or reviewer>
- <Any follow-up ticket opened or updated>
