# Phase & Agent Transition — Multi-Agent Relay Protocol

Use this skill when a project phase is complete and the user needs to switch to a different AI agent (e.g., from a Strategy Agent to a Development Agent).

---

## 📋 The Phase Transition Package Template

When the user says "Ready for the next phase" or when a phase transition occurs, generate a message using this exact structure:

---
### 📦 AI KIT BASE: PHASE TRANSITION PACKAGE

**1. Project State**
- **ID**: `[PROJECT_ID]`
- **Mode**: `[OPERATION_MODE]`
- **Current Phase**: `[e.g., PHASE 1: FOUNDATION]`
- **Target Phase**: `[e.g., PHASE 2: BUILD]`
- **Work Category**: `[e.g., DEVELOPMENT]`
- **Infrastructure Ready**: `[YES/NO] (Verify Supabase/Vercel/ENV)`

**2. Files to Read**
- Primary Source of Truth: `[ID]-STATUS.md`
- Logic/Design Truth: `[ID]-BRAND.md`, `[ID]-ARCHITECTURE.md`
- Config Truth: `.env.example`

**3. Instructions for the New Agent**
- **Target Role**: `[e.g., Agent specialized in DEVELOPMENT]`
- **Context**: `[1-sentence summary of what has been decided/built]`
- **Next Milestone**: `[Next task from STATUS file]`

**4. Required Skills to Load**
- `kit/skills/core-workflow/INSTRUCTIONS.md`
- `kit/skills/[next-skill]/INSTRUCTIONS.md`
---

## 🗺️ Standard Transitions (The Golden Path)

### Path 1: PHASE 1 (STRATEGY) → PHASE 2 (DEVELOPMENT)
- **When**: Brand is stable, Architecture is designed.
- **Agent Switch**: Highly recommended if using a specialized code-terminal agent.
- **Focus**: Implementation, naming conventions, clean UI.

### Path 2: PHASE 2 (DEVELOPMENT) → PHASE 3 (QUALITY)
- **When**: Feature is built and functional.
- **Agent Switch**: Optional, but good for a fresh "audit" perspective.
- **Focus**: Security, performance, refactoring.

### Path 3: PHASE 3 (QUALITY) → PHASE 4 (CONTENT)
- **When**: Code is STABLE.
- **Agent Switch**: Recommended to switch to a specialized content/SEO agent to save coding tokens.
- **Focus**: SEO (`web-seo` per-page verification, then `web-deploy` launch checklist), Copywriting, User Documentation (`core-documentation`).

## 🗺️ Handoff Verification

Once the phase transition package is generated:
1. **Wait for user** to confirm they have transitioned to the new agent/tool.
2. **Warn on token efficiency**: Remind the user that switching to a simpler agent for Phase 4 (CONTENT) saves cost and prevents unnecessary context loading.
