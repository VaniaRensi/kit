---
name: workflow-ai
description: Guides the complete development process of a project with AI. Use this skill at the start of every new project, or when the user says "let's start", "new project", "let's go", "modify this", "update this file". Manages kickoff, work phases, planned and improvised checkpoints, autonomous loops, and modifications to existing code. Contains the communication protocol between user and AI for the entire project lifecycle.
---

# AI Workflow — The Golden Path Protocol

This protocol governs the project lifecycle. It enforces a linear, structured progression (The Golden Path) to ensure quality and focus.

---

## 🗺️ The Golden Path (Phases)

You must work within the boundaries of the `CURRENT_PHASE` defined in `[ID]-STATUS.md`:

1.  **FASE 0: CONFIG (Agnostico)**: Initial setup, project ID, stack selection, and git init.
2. ### 🛠️ FASE 1: FONDAMENTA (Kickoff Strategico)
L'obiettivo è definire la visione. Prima di generare l'Handoff per la fase di codice, DEVI verificare che l'utente sia pronto tecnicamente:
1. **Infrastructure Check**: "Hai già creato gli account necessari (Supabase, Vercel, Firebase)?".
2. **Environment Ready**: "Hai accesso alle chiavi API/Variabili d'ambiente?".
3. **Asset Preparation**: Guida l'utente nella creazione degli account e dei database mentre sei ancora in modalità STRATEGIA. È più economico e meno frustrante.

**NON procedere alla Fase 2 (SVILUPPO) finché questi asset non sono pronti.**
3.  **FASE 2: COSTRUZIONE (SVILUPPO)**: Pure implementation of components, logic, and UI.
4.  **FASE 3: CONTROLLO (QUALITÀ)**: Security audits, refactoring, and stability verification.
5.  **FASE 4: LANCIO (CONTENUTI)**: SEO, final copy, and user documentation.

**🚨 Phase-Gate Protocol**: Ogni Milestone deve concludersi con un Audit completo (Tabella Checkpoint) PRIMA di poter pianificare la Milestone successiva. Non saltare mai questa fase.

---

## 🚦 Phase Gates & Transition

Before moving to a new phase, you MUST verify that the current phase's goals are met.

- **Phase Gate Protocol**: If the user asks to start a task from a future phase while the current phase is incomplete, you MUST warn them:
  > "Attenzione: siamo ancora in `[FASE CORRENTE]`. Saltare alla `[FASE RICHIESTA]` potrebbe causare disallineamenti tecnici o di brand. Vuoi procedere comunque o finiamo prima `[OBIETTIVO CORRENTE]`?"

---

## 🚀 Execution Cycle (The Loop)

Every task follows this loop:

1.  **Initialization Statement**: Start the response with:
    > "Sto utilizzando le skill: `[skill]`. Fase: `[FASE]`. Categoria: `[CATEGORIA]`."
2.  **Confirm Goal**: State what is being developed in this milestone.
3.  **Autonomous Build**: Maximum 2 attempts to solve errors before asking the user.
4.  **Checkpoint**: Once stable, propose the quality/security review.
5.  **Commit**: Propose a structured commit message for the stable work.

---

## ⚙️ Environment & Routing

Your behavior is driven by the variables in `[ID]-STATUS.md`.

- **IF `CURRENT_PHASE == FASE 1`**: Load `brand-discovery` or `core-architecture`.
- **IF `CURRENT_PHASE == FASE 2`**: Load `web-ux-ui`, `web-design-tokens`.
- **IF `CURRENT_PHASE == FASE 3`**: Load `core-quality`, `core-naming`.
- **IF `CURRENT_PHASE == FASE 4`**: Load `core-documentation`, `core-ux` (SEO).

---

## 🏁 Session End (Mandatory)

1.  Update `[ID]-STATUS.md`: mark milestones as STABLE or IN PROGRESS.
2.  Update `CURRENT_PHASE` if a transition occurred.
3.  Add entry to `[ID]-HISTORY.md` summarizing logical decisions and pivots.
