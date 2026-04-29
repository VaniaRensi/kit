---
name: workflow-ai
description: Guides the complete development process of a project with AI. Use this skill at the start of every new project, or when the user says "let's start", "new project", "let's go", "modify this", "update this file". Manages kickoff, work phases, planned and improvised checkpoints, autonomous loops, and modifications to existing code. Contains the communication protocol between user and AI for the entire project lifecycle.
---

# AI Workflow — The Golden Path Protocol

This protocol governs the project lifecycle. It enforces a linear, structured progression (The Golden Path) to ensure quality and focus.

---

## 🗺️ The Golden Path (Phases)

You must work within the boundaries of the `CURRENT_PHASE` defined in `[ID]-STATUS.md`:

1. **PHASE 0: CONFIG**: Initial setup, project ID, stack selection. Git is a prerequisite — do NOT teach the user how to set it up.
2. **PHASE 1: FOUNDATION (STRATEGY)**: Define the vision. Before generating any handoff for the build phase, you MUST verify the user is technically ready:
   1. **Infrastructure Check**: "Have you already created the necessary accounts (Supabase, Vercel, Firebase)?"
   2. **Environment Ready**: "Do you have access to your API keys and environment variables?"
   3. **Asset Preparation**: Guide the user to verify accounts and databases while still in STRATEGY mode. This is cheaper and less frustrating than discovering missing assets mid-build.

   **DO NOT proceed to Phase 2 (BUILD) until all assets are confirmed ready.**
3. **PHASE 2: BUILD (DEVELOPMENT)**: Pure implementation of components, logic, and UI.
4. **PHASE 3: CONTROL (QUALITY)**: Security audits, refactoring, and stability verification.
5. **PHASE 4: LAUNCH (CONTENT)**: SEO, final copy, and user documentation.

**🚨 Phase-Gate Protocol**: Every Milestone MUST end with a complete Audit (Checkpoint Summary Table) BEFORE the next Milestone can be planned. Never skip this step.

---

## 🚦 Phase Gates & Transition

Before moving to a new phase, you MUST verify that the current phase's goals are met.

- **Phase Gate Protocol**: If the user asks to start a task from a future phase while the current phase is incomplete, you MUST warn them:
  > "Warning: we are still in `[CURRENT PHASE]`. Jumping to `[REQUESTED PHASE]` could cause technical or brand misalignment. Do you want to proceed anyway, or should we finish `[CURRENT GOAL]` first?"

---

## 🚀 Execution Cycle (The Loop)

Every task follows this loop:

1. **Initialization Statement**: Start the response with:
   > "Skills: `[skill-list]`. Phase: `[PHASE]`. Category: `[CATEGORY]`. Design: `[Brand/UX Status]`. App Lang: `[APP_LANG]`. Chat Lang: `[CHAT_LANG]`."
2. **Confirm Goal**: State what is being developed in this milestone.
3. **Autonomous Build**: Maximum 2 attempts to solve errors before asking the user.
4. **Checkpoint**: Once stable, propose the quality/security review.
5. **Commit**: Propose a structured commit message for the stable work.

---

## ⚙️ Environment & Routing

Your behavior is driven by the variables in `[ID]-STATUS.md`.

- **IF `CURRENT_PHASE == PHASE 1`**: Load `brand-discovery` or `core-architecture`.
- **IF `CURRENT_PHASE == PHASE 2`**: Load `web-ux-ui`, `web-design-tokens`.
- **IF `CURRENT_PHASE == PHASE 3`**: Load `core-quality`, `core-naming`.
- **IF `CURRENT_PHASE == PHASE 4`**: Load `core-documentation`, `core-ux` (SEO).

---

## 🏁 Session End (Mandatory)

1. Update `[ID]-STATUS.md`: mark milestones as STABLE or IN PROGRESS.
2. Update `CURRENT_PHASE` if a transition occurred.
3. Add entry to `[ID]-HISTORY.md` summarizing logical decisions and pivots.
