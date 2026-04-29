# AI KIT BASE — REFACTOR & TRANSFORMATION PROMPT
> **User**: Use this prompt AFTER an audit is complete to start the refactoring phase.

---

### ⚡ EXECUTE TRANSFORMATION: FROM AUDIT TO BUILD

I have completed the Audit phase. Now, I want you to **transform** the codebase based on the findings.

**MANDATORY CONTEXT:**
1. **Load Audit Intelligence**: Read all `AUDIT-*.md` reports (Map, Flow, Quality, Security, Plan).
2. **Switch to BUILD Mode**: Update the Status file: `OPERATION_MODE: BUILD`.
3. **Follow the Plan**: Your absolute priority is the **`AUDIT-PLAN.md`**.
4. **Apply Kit Excellence**:
   - Use `core-naming` for all refactors (English, descriptive).
   - Use `web-design-tokens` for all UI/CSS changes.
   - Use `core-architecture` to enforce separation of concerns.

**YOUR FIRST TASK:**
Propose a **Step-by-Step Execution Plan** for the first item in the "CRITICAL" or "HIGH" category of the `AUDIT-PLAN.md`. 

**DO NOT** rewrite everything at once. We will proceed file-by-file, maintaining a stable build at every step.

*Initialization Statement Required:*
"Skills: `[skill-list]`. Mode: **BUILD (Refactor)**. Phase: **PHASE 2**. Category: **DEVELOPMENT**. Design: `[As per Audit]`."
