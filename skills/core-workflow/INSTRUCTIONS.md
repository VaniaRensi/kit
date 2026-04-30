---
name: workflow-ai
description: Guides the complete project lifecycle using the 3-Mode Engine (BUILD, AUDIT, DOCUMENT). Manages kickoff, phase gates, and routing.
---

# AI Workflow — The 3-Mode Engine

This protocol governs the project lifecycle. It adapts its linear progression based on the selected `OPERATION_MODE`.

---

## 🗺️ Operation Modes

You must operate within one of these three modes:

1.  **🏗️ BUILD**: For new projects. Follows the standard **Golden Path (F0-F4)**.
2.  **🔍 AUDIT**: For existing codebases. Focuses on **Phase 1 (Discovery)** and **Phase 3 (Audit)**. Produces the 5 Audit Reports.
3.  **📚 DOCUMENT**: For generating project documentation. Jumps straight to **Phase 4 (Launch)** logic.

---

## 🗺️ The Golden Path (Phases)

You must work within the boundaries of the `CURRENT_PHASE` defined in `[ID]-STATUS.md`:

1.  **PHASE 0: CONFIG**: Setup and Initialization. Prerequisites: GitHub repo and API keys.
2.  **PHASE 1: FOUNDATION (STRATEGY)**: 
    - **BUILD mode**: Branding, UX, and Architecture.
    - **AUDIT mode**: Mapping and Logic Flow analysis.
3.  **PHASE 2: BUILD (DEVELOPMENT)**: 
    - **BUILD mode**: Pure implementation of UI and logic.
    - **AUDIT mode**: Optional "Refactor" phase after the audit plan is approved.
4.  **PHASE 3: CONTROL (QUALITY)**: 
    - **BUILD mode**: Standard checkpoint and security sweep.
    - **AUDIT mode**: The core phase where the 5 Reports are generated.
5.  **PHASE 4: LAUNCH (CONTENT)**: 
    - **ALL modes**: SEO, User Documentation, and Final Handover.

**🚨 Phase-Gate Protocol**: Every Milestone MUST end with a complete Audit (Checkpoint Summary Table) BEFORE the next Milestone can be planned.

---

## 🚦 Phase Gates & Transition

- **Mode Drift**: If a user asks to "build" while in "AUDIT" mode, suggest switching `OPERATION_MODE` in the status file before proceeding.
- **Phase Warning**: If jumping phases:
  > "Warning: we are still in `[CURRENT PHASE]`. Jumping to `[REQUESTED PHASE]` could cause technical debt. Proceed?"

---

## 🚀 Execution Cycle (The Loop)

> **Initialization Statement format** is defined in `kit/MASTER-RULES.md` — that is the single source of truth. Do not redefine it here.

Every task follows this loop:

1.  **Initialization Statement**: Output the statement as defined in `MASTER-RULES.md`.
2.  **Confirm Goal**: State the specific milestone being worked on.
3.  **Checkpoint**: Once stable, run the `core-quality` or `core-audit` checks.

---

## ⚙️ Routing Logic

Your behavior is driven by `OPERATION_MODE` and `CURRENT_PHASE`:

- **IF `MODE == BUILD`**:
  - `F0` (setup) → detect language stack: if a `lang-*` skill matches the project (e.g. `lang-csharp` for `.csproj`), load it now and keep it active for F2/F3.
  - `F1` -> `brand-discovery`, `core-architecture`.
  - `F2` -> `web-ux-ui`, `web-design-tokens`, `web-seo` (per page: content, metadata, images).
  - `F3` -> `core-quality`.
  - `F4` -> `web-seo` (verify all pages), `web-deploy` (launch checklist), `core-documentation`.
- **IF `MODE == AUDIT`**:
  - `F1` -> `core-audit` (Map & Flow).
  - `F3` -> `core-audit` (Quality, Security, Deps, Plan).
  - `F2` (after plan approved) -> `core-refactor` (execute AUDIT-PLAN.md).
- **IF `MODE == DOCUMENT`**:
  - `F4` -> `core-documentation`.

---

## 🏁 Session End (Mandatory)

1.  Update `[ID]-STATUS.md`: mark milestones and `CURRENT_PHASE`.
2.  Add entry to `[ID]-HISTORY.md` summarizing logical decisions.
