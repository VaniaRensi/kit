---
name: core-refactor
category: quality
description: >
  Executes the Refactor Directive from [ID]-AUDIT-v[N]/PLAYBOOK.md, fix-by-fix (CRITICAL → HIGH → MEDIUM → LOW).
  All rewritten files go into a versioned [ID]-REFACTOR-v[N]/ sandbox — originals are never touched.
  Produces SWAP-GUIDE.md inside the sandbox with exact commands to apply changes when approved.
  Primary input: [ID]-AUDIT-v[N]/PLAYBOOK.md. Never run without it.
---

# Refactor Engine — Systematic Code Rewriting

This skill executes what the audit already planned. Your primary input is `[ID]-AUDIT-v[N]/PLAYBOOK.md` — it tells you which fixes to make, in what order, and which skill governs each one. You do not re-analyze the codebase. You execute.

**Two cardinal rules:**
1. **Originals are sacred** — every rewritten file goes into `[ID]-REFACTOR-v[N]/`. Never touch the source.
2. **Scope is sacred** — fix only what the Playbook identified. Nothing else.

---

## 🗂️ The Refactor Sandbox

All work happens inside a dedicated mirror folder at the project root.

```
[project-root]/
├── src/                            ← ORIGINAL — never touched, reference only
├── [ID]-AUDIT-v1/                  ← audit outputs (read-only reference)
│   ├── PLAYBOOK.md                 ← your primary input
│   └── AUDIT-PLAN.md               ← detailed fix list (reference when you need detail)
├── [ID]-REFACTOR-v1/               ← SANDBOX — all rewritten files go here
│   ├── src/
│   │   └── [only changed files, mirroring original paths]
│   └── SWAP-GUIDE.md               ← generated as fixes complete
```

**Version rule**: match the refactor version to the audit version you are executing. If running from `[ID]-AUDIT-v2/PLAYBOOK.md`, create `[ID]-REFACTOR-v2/`. Check for existing `[ID]-REFACTOR-v*/` folders and increment if needed.

**Mirror only files being changed.** Preserve the exact same relative path as the original.

---

## 🚦 Pre-Flight Check

Before the first fix, confirm all of these:

- [ ] `[ID]-AUDIT-v[N]/PLAYBOOK.md` exists and has been approved by the user.
- [ ] `[ID]-AUDIT-v[N]/AUDIT-PLAN.md` exists for detailed reference.
- [ ] User has confirmed: *"Proceed with refactor"* — do not self-start.
- [ ] `[ID]-REFACTOR-v[N]/` folder created (version matches the audit being executed).
- [ ] `[ID]-REFACTOR-v[N]/SWAP-GUIDE.md` initialized (see template below).
- [ ] `[ID]-STATUS.md` updated: `OPERATION_MODE: BUILD`, `CURRENT_PHASE: PHASE 2`.

### Initialize `[ID]-REFACTOR-v[N]/SWAP-GUIDE.md`
```markdown
# Swap Guide — [PROJECT_ID] v[N]
> Based on: [ID]-AUDIT-v[N]/PLAYBOOK.md
> Run these commands ONLY after reviewing and approving all files in [ID]-REFACTOR-v[N]/.

## ⚠️ Before You Swap
- [ ] Review every file in `[ID]-REFACTOR-v[N]/` against its original
- [ ] Confirm the project still runs from the original
- [ ] core-quality checkpoint passed

## Swap Commands
[filled automatically as fixes complete — one line per changed file]

## After Swap
1. Archive `[ID]-REFACTOR-v[N]/` (do not delete — keep for reference)
2. Run the project and verify
```

---

## ⚙️ The Execution Loop (One Fix at a Time)

Read the **Refactor Directive** section of `[ID]-AUDIT-v[N]/PLAYBOOK.md`. Work through it in order: CRITICAL → HIGH → MEDIUM → LOW.

### Step 1 — Declare
Before touching any file, state:
> "**Fix [N]/[total]** `[LEVEL]`: `[file/path.ts]`
> **Problem**: [from Playbook]
> **Scope**: I will only touch [specific function / section / lines].
> **Skill**: loading `[skill-name]` for this fix type.
> **Verification**: [how I will confirm behavior is preserved]"

### Step 2 — Read the Standard
Load the skill referenced in the Playbook for this fix. Read the relevant section. This is the quality bar your rewrite must meet — do not work from memory.

### Step 3 — Read the Original
Read the source file as reference. Only the files this fix needs.

### Step 4 — Write to Sandbox
Create the rewritten file at `[ID]-REFACTOR/[original/path/file.ext]`.
- Fix only the identified problem.
- If the fix reveals a new issue not in the Playbook, add it as LOW in `[ID]-AUDIT-v[N]/AUDIT-PLAN.md` and continue.
- Do not mix refactor with feature additions.

### Step 5 — Verify
Compare new file against original:
- State what behavior is preserved.
- State what changed and why it meets the skill's standard.
- If tests exist: run them. If not: describe the manual check.

### Step 6 — Update Records
**`[ID]-AUDIT-v[N]/AUDIT-PLAN.md`**:
```
- [x] [LEVEL] `file/path.ts` — description ✅ Fixed [date]
```
**`[ID]-REFACTOR-v[N]/SWAP-GUIDE.md`** — add the swap command:
```bash
# Fix: [short description]
cp [ID]-REFACTOR-v[N]/src/services/user.ts src/services/user.ts
```

### Step 7 — Checkpoint Gate
After all **CRITICAL** items → run `core-quality` before advancing to HIGH.
After all **HIGH** items → run `core-quality` before advancing to MEDIUM.
MEDIUM and LOW can share a final checkpoint.

---

## 📚 Skills — On-Demand Reference

The Playbook already tells you which skill to load for each fix. This table is a quick lookup.

| Fix Category | Skill | What It Defines |
|---|---|---|
| Naming violations | `core-naming` | Variables, functions, files, DB columns |
| Architecture violations | `core-architecture` | Separation of concerns, structure, size limits |
| Missing design tokens | `web-design-tokens` | 3-layer token system + migration protocol |
| Component patterns | `web-ux-ui` | Accessible primitives, layout systems |
| UX / accessibility | `core-ux` | 8 UX principles, hierarchy, capitalisation |
| Security vulnerabilities | `core-quality` §Security | RLS, env vars, sanitization, auth |
| Documentation gaps | `core-documentation` | What/how to document |
| Architecture decision needed | `core-architecture` | Stop — redesign first, then return |
| Language-specific conventions | `lang-[language]` (e.g. `lang-csharp`) | Naming, patterns, security for that stack |

---

## 🛡️ Scope Control

| Situation | Rule |
|---|---|
| Unrelated bug spotted | Add to `AUDIT-PLAN.md` as LOW. Do not fix now. |
| Fix requires touching a STABLE file | Warn user. Proceed only with explicit approval. |
| Fix would change a public API | Stop. Load `core-architecture` — redesign first. |
| Fix takes >30 lines of change | Split into two items in `AUDIT-PLAN.md`. |
| User asks to add a feature | Decline. Features come after refactor is STABLE and swapped. |

---

## 📋 Progress Report

After every 5 fixes or at end of a priority level:

```
## Refactor Progress — [date]

| Priority | Total | Done | Remaining |
|----------|-------|------|-----------|
| CRITICAL | N     | N    | 0         |
| HIGH     | N     | N    | N         |
| MEDIUM   | N     | N    | N         |
| LOW      | N     | N    | N         |

Sandbox: [ID]-REFACTOR/ ([N] files)
Next: [next item]
```

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 2: BUILD (bridging from AUDIT mode).
2. **Objective**: Produce a complete, reviewable `[ID]-REFACTOR/` and `SWAP-GUIDE.md`.
3. **Recommended Next Step**:
   - All CRITICAL/HIGH done → `kit/skills/core-quality/INSTRUCTIONS.md` checkpoint.
   - Full plan complete, user approves → user runs `SWAP-GUIDE.md`, then load `kit/skills/core-documentation/INSTRUCTIONS.md`.
   - New architectural issue → load `kit/skills/core-architecture/INSTRUCTIONS.md`.
4. **Flow**: `core-audit → [ID]-PLAYBOOK.md → core-refactor → core-quality → core-documentation`
