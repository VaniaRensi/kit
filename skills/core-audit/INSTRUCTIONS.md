---
name: core-audit
category: quality
description: Systematic analysis of an existing codebase across 5 dimensions (Map, Flow, Quality, Security, Plan). Use this skill when the user selects "AUDIT" mode or asks to "analyze this existing app". Focuses on understanding before changing.
---

# Audit Engine — Systematic Codebase Analysis

Use this skill to perform a professional-grade audit of an existing software project. The audit is non-destructive and results in a standardized documentation set.

---

## 🗺️ The 5-Report Framework

Every audit MUST produce these five files in the root directory, prefixed with `AUDIT-`.

### 1. `AUDIT-MAP.md` (What exists?)
- **Goal**: Full inventory of the project.
- **Content**:
  - Tech Stack (Frameworks, DB, Auth).
  - Folder Structure Analysis (Tree).
  - External Dependencies (Significant ones).
  - Entry Points (Main files, API routes).

### 2. `AUDIT-FLOW.md` (How does data move?)
- **Goal**: Understand logic and state.
- **Content**:
  - Key User Flows (e.g., Auth flow, Payment flow).
  - Data Models (Tables/Schemas).
  - Component Hierarchy (Frontend).
  - State Management approach.

### 3. `AUDIT-QUALITY.md` (Code Health)
- **Goal**: Evaluate against AI Kit Base standards.
- **Content**:
  - Naming Convention Review (English? Descriptive?).
  - Architecture Review (Separation of concerns?).
  - UI/UX Review (Tokens? Hierarchy?).
  - Performance Hotspots (Visual bloat, heavy bundles).

### 4. `AUDIT-SECURITY.md` (Safety Scan)
- **Goal**: Identify critical vulnerabilities.
- **Content**:
  - Env Var exposure check.
  - Auth/Permission logic verification.
  - Input Sanitization review.
  - Dependency Vulnerability check (`npm audit` if applicable).

### 5. `AUDIT-PLAN.md` (Prioritized Action)
- **Goal**: Roadmap for improvement.
- **Content**:
  - **CRITICAL**: Immediate fixes needed.
  - **HIGH**: Architecture/Naming refactors.
  - **MEDIUM**: Feature additions or UX polish.
  - **LOW**: Minor tweaks.

---

## 🚦 Audit Workflow

1.  **Exploration**: Run `ls -R` and read `package.json` / `requirements.txt`.
2.  **Mapping**: Build the `AUDIT-MAP.md` and `AUDIT-FLOW.md`.
3.  **Deep Dive**: Sample 3-5 files per layer (UI, Service, Data) to evaluate quality.
4.  **Reporting**: Finalize all 5 reports.
5.  **Transition**: Once reports are STABLE, suggest moving to `BUILD` mode to execute the `AUDIT-PLAN.md`.

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 1: FOUNDATION (Mode: **AUDIT**).
2. **Objective**: Understand the "As-Is" state before any "To-Be" changes.
3. **Recommended Next Step**:
   - If reports are complete → Load `AUDIT-PLAN.md` and switch to `BUILD` mode.
4. **Tool Tip**: An "Auditor" agent is perfect for this—it shouldn't fix code, only document what's wrong first.
