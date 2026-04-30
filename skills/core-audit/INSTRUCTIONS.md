---
name: core-audit
category: quality
description: Systematic analysis of an existing codebase across 6 dimensions (Map, Flow, Quality, Security, Deps, Plan). Use this skill when the user selects "AUDIT" mode or asks to "analyze this existing app". Focuses on understanding before changing.
---

# Audit Engine — Systematic Codebase Analysis

Use this skill to perform a professional-grade audit of an existing software project. The audit is non-destructive and results in a standardized documentation set.

---

## 🗺️ The 6-Report Framework

Every audit MUST produce these six files in the root directory, prefixed with `AUDIT-`.

### 1. `AUDIT-MAP.md` (What exists?)
- **Goal**: Full inventory of the project.
- **Content**:
  - Tech Stack (Frameworks, DB, Auth).
  - Folder Structure Analysis (Tree).
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
  - SQL / NoSQL injection risks.

### 5. `AUDIT-DEPS.md` (Dependency Health)
- **Goal**: Surface risks from third-party packages.
- **Content**:
  - Run the appropriate scanner for the tech stack and record output:
    - **Node.js**: `npm audit --json`
    - **Python**: `pip-audit`
    - **Ruby**: `bundle audit`
    - **C# / .NET**: `dotnet list package --vulnerable` + `dotnet list package --outdated`
  - Outdated critical dependencies (flag anything >2 major versions behind).
  - Unused or duplicate dependencies (`depcheck` or equivalent).
  - License risks (GPL in a commercial project, etc.).
  - Lock-file status (is `package-lock.json` / `yarn.lock` / `packages.lock.json` committed?).

### 6. `AUDIT-PLAN.md` (Prioritized Action)
- **Goal**: Roadmap for improvement, feeding directly into `core-refactor`.
- **Content**:
  - **CRITICAL**: Security vulnerabilities or broken functionality — fix immediately.
  - **HIGH**: Architecture violations, naming refactors, dependency CVEs.
  - **MEDIUM**: Feature additions, UX polish, outdated-but-stable deps.
  - **LOW**: Minor tweaks, optional improvements.
- **Format per item**:
  ```
  - [ ] [LEVEL] `file/path.ts` — short description of the problem
        Reason: why this is a risk or debt
        Fix: the specific change required
  ```

---

## 🚦 Audit Workflow

1.  **Exploration**: Run `ls -R` and read the dependency manifest (`package.json`, `requirements.txt`, `*.csproj`, `Gemfile`, etc.). Then check for language-specific skill indicators:
    - `.csproj` or `.sln` found → load `kit/skills/lang-csharp/INSTRUCTIONS.md` before continuing.
    - `requirements.txt` or `pyproject.toml` found → check for `lang-python` skill.
    - `go.mod` found → check for `lang-go` skill.
    If a matching `lang-*` skill exists, load it now and apply its lens throughout the rest of the audit.
2.  **Dependency Scan**: Run the appropriate scanner (see AUDIT-DEPS section above) and save raw output.
3.  **Mapping**: Build `AUDIT-MAP.md` and `AUDIT-FLOW.md`.
4.  **Deep Dive**: Sample 3–5 files per layer (UI, Service, Data) to evaluate quality and security.
5.  **Reporting**: Finalize all 6 reports. Do NOT write `AUDIT-PLAN.md` until the other 5 are stable — the plan is a synthesis of the findings.
6.  **Transition**: Once all 6 reports are STABLE, present a summary and load `core-refactor` to execute the plan.

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 3: CONTROL (Mode: **AUDIT**).
2. **Objective**: Produce the complete 6-Report set before any code changes.
3. **Recommended Next Step**:
   - If all 6 reports are complete → Load `kit/skills/core-refactor/INSTRUCTIONS.md` and execute `AUDIT-PLAN.md`.
   - If still mapping → Continue building reports in order (1→6).
4. **Tool Tip**: An "Auditor" agent reads only — it must not fix code. Keep audit and refactor as separate steps so findings are never lost.
