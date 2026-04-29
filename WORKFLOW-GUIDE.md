# The Golden Path — Guide to Structured AI Workflow

This document explains the "engine" of the AI Kit Base and how to navigate projects using specialized agents and structured phases.

## 🗺️ The 5 Phases (Timeline)

```mermaid
graph TD
    F0[PHASE 0: CONFIG] -->|Init Status| F1[PHASE 1: FOUNDATION]
    F1 -->|Stable Brand & Arch| F2[PHASE 2: BUILD]
    F2 -->|Functional Feature| F3[PHASE 3: CONTROL]
    F3 -->|Stable Code| F4[PHASE 4: LAUNCH]
    F4 -->|Production Ready| END(Project Complete)

    subgraph "STRATEGY"
    F1
    end

    subgraph "DEVELOPMENT"
    F2
    end

    subgraph "QUALITY"
    F3
    end

    subgraph "CONTENT"
    F4
    end
```

## 🤖 Agent Specialization & Handoffs

The AI Kit is designed for a **Multi-Agent Relay**. Each phase is an opportunity to switch to the most efficient tool for the job.

| Phase | Recommended Agent Role | Why Switch? |
| :--- | :--- | :--- |
| **PHASE 1: STRATEGY** | Architect / Strategist | Better at broad vision and UX theory. |
| **PHASE 2: DEVELOPMENT** | Builder / Terminal Coder | Faster at multi-file edits and terminal tasks. |
| **PHASE 3: QUALITY** | Auditor / Quality Agent | Fresh perspective on security and performance. |
| **PHASE 4: CONTENT** | Content / SEO Specialist | Specialized in copywriting; saves coding tokens. |

## ⚙️ How the Engine Works (Mind Map)

1. **Initial Prompt**: User points the agent to the `PROMPT.md` entry point.
2. **Master Rules**: The agent loads `MASTER-RULES.md`, establishing the "Agnostic Awareness".
3. **Status Reading**: The agent reads `[ID]-STATUS.md` to find its location on the **Golden Path**.
4. **Skill Loading**: Based on the `CURRENT_PHASE`, the agent loads the relevant skills.
5. **Initialization Statement**: The agent confirms its status: *"Skill: X, Phase: Y, Category: Z"*.
6. **Handoff / Drift**: If the user's request changes the category, the agent triggers **Drift Detection** and suggests a transition.
7. **Historification**: Every major decision is logged in `[ID]-HISTORY.md` to ensure session continuity.

---
*Follow the Golden Path. Don't jump. Build to last.*
