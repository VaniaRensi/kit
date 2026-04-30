---
name: core-refactor
category: quality
description: >
  Executes AUDIT-PLAN.md fix-by-fix, in priority order (CRITICAL → HIGH → MEDIUM → LOW).
  Use immediately after core-audit produces its 6 reports. One item at a time, checkpoint
  before advancing levels. Never run without a completed AUDIT-PLAN.md.
---

# Refactor Engine — Systematic Code Rewriting

This skill translates audit findings into actual code changes. It runs after `core-audit` and before `core-quality` (final checkpoint). The cardinal rule: **scope is sacred** — fix only what the audit identified, nothing else.

---

## 🚦 Pre-Flight Check (Before Any Fix)

Before the first change, confirm these are all true:

- [ ] `AUDIT-PLAN.md` exists and all 6 audit reports are STABLE.
- [ ] The user has confirmed: *"Proceed with refactor"* (do not self-start).
- [ ] The project builds and runs as-is (establish a known-good baseline).
- [ ] `[ID]-STATUS.md` is updated: `OPERATION_MODE: BUILD`, `CURRENT_PHASE: PHASE 2`.

If any item is false, stop and resolve it before continuing.

---

## ⚙️ The Execution Loop (One Fix at a Time)

For **every item** in `AUDIT-PLAN.md`, in order CRITICAL → HIGH → MEDIUM → LOW:

### Step 1 — Declare
State the item explicitly before touching any file:

> "**Fix [N]/[total]** `[LEVEL]`: `[file/path.ts]`
> **Problem**: [what AUDIT-PLAN says is wrong]
> **Scope**: I will only touch [specific function / section / lines].
> **Verification plan**: [how I will confirm behavior is preserved]"

### Step 2 — Read
Read the specific file(s). Do not read the entire codebase — only what this fix needs.

### Step 3 — Apply
Make the change. Rules:
- Fix **only** the identified problem. Do not opportunistically clean nearby code.
- If the fix reveals a new problem not in `AUDIT-PLAN.md`, do NOT fix it now — add it as a new LOW item in `AUDIT-PLAN.md` and continue.
- Do not mix a refactor with a feature addition in the same step.

### Step 4 — Verify
Confirm the fix is correct:
- State explicitly what behavior is preserved.
- If tests exist: run them and report the result.
- If no tests exist: describe the manual check the user should do before marking STABLE.

### Step 5 — Mark Done
Update `AUDIT-PLAN.md` — check the item:
```
- [x] [LEVEL] `file/path.ts` — description ✅ Fixed [date]
```

### Step 6 — Checkpoint Gate (between levels)
After completing **all CRITICAL items**, STOP and run `core-quality` before moving to HIGH.
After completing **all HIGH items**, STOP and run `core-quality` before moving to MEDIUM.
MEDIUM and LOW can be batched into a single final checkpoint.

> "All CRITICAL fixes are complete. Running `core-quality` checkpoint before advancing to HIGH priority items."

---

## 📚 Standards Reference

Before applying any fix, load the skill that owns the standard you are fixing against. Do not invent criteria — the skill is the source of truth.

| Fix Category | Skill to Load |
|-------------|---------------|
| Naming (variables, functions, classes) | `core-naming` |
| Architecture (separation of concerns, patterns) | `core-architecture` |
| UI layout, tokens, component structure | `web-ux-ui` + `web-design-tokens` |
| UX principles, accessibility, hierarchy | `core-ux` |
| Security vulnerabilities | `core-quality` |
| Language-specific conventions (.NET, Python, etc.) | `lang-[language]` (e.g. `lang-csharp`) |

Load only the skill relevant to the current fix. Do not load all skills upfront.

---

## 🛡️ Scope Control Rules

These rules prevent refactor drift — the #1 cause of regressions:

| Situation | Rule |
|-----------|------|
| You spot an unrelated bug while fixing | Add it to AUDIT-PLAN.md as LOW. Do not fix now. |
| A fix requires touching a STABLE file | Warn the user. Proceed only with explicit approval. |
| The fix would change a public API/interface | Stop. This needs an architecture decision — load `core-architecture`. |
| A fix takes >30 lines of change | Split it into two items in AUDIT-PLAN.md. |
| User asks to add a feature mid-refactor | Decline politely. Features go in PHASE 2 after refactor is STABLE. |

---

## 📋 Refactor Progress Report

After every 5 fixes (or at the end of a priority level), output a progress table:

```
## Refactor Progress — [date]

| Priority | Total | Done | Remaining |
|----------|-------|------|-----------|
| CRITICAL | N     | N    | 0         |
| HIGH     | N     | N    | N         |
| MEDIUM   | N     | N    | N         |
| LOW      | N     | N    | N         |

Next: [next item description]
```

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 2: BUILD (Mode: **BUILD** / bridging from **AUDIT**).
2. **Objective**: Execute every item in `AUDIT-PLAN.md` without introducing new regressions.
3. **Recommended Next Step**:
   - After all CRITICAL/HIGH items → Run `kit/skills/core-quality/INSTRUCTIONS.md` checkpoint.
   - After full plan is complete → Load `kit/skills/core-documentation/INSTRUCTIONS.md` (Phase 4: LAUNCH).
   - If new architectural issues surface → Load `kit/skills/core-architecture/INSTRUCTIONS.md`.
4. **Tool Tip**: This is the most dangerous phase for scope creep. A terminal agent (Claude Code) is ideal here — it reads and writes code, stays in the file, and doesn't drift into design conversations.
