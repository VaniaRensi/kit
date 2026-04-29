---
name: web-design-tokens
category: development
description: Technical design system architecture using semantic tokens and fluid scaling.
---

# Design Tokens — Technical System Architecture

Use this skill to transform a Brand Brief into a functional, maintainable design system using semantic tokens and fluid scaling.

## 1. The 3-Layer Architecture
You must organize the system in three layers to ensure it is rebrandable and supports dark mode effortlessly.

1.  **Primitives**: Raw values (e.g., `--blue-500: oklch(55% 0.2 250)`). These are the "ink".
2.  **Semantics**: Meaningful roles (e.g., `--color-primary: var(--blue-500)`). This is the "pen".
3.  **Components**: Contextual values (e.g., `--button-bg: var(--color-primary)`). This is the "writing".

## 2. Derived Variance (Shades & Alpha)
Do NOT pick ad-hoc colors for UI states. Derive them from the core palette:
- **States (Hover/Active)**: Use a lighter or darker shade from the same hue scale.
- **Surfaces & Borders**: Use the `oklch` relative syntax to apply transparency: `oklch(from var(--color-primary) l c h / 0.1)`.

## 3. Fluid Geometry
Use `clamp()` for spacing and typography to eliminate the need for media queries:
- **Spacing**: `gap-grid`, `p-card`, `py-section`.
- **Typography**: `text-heading-lg`, `text-body`.

## 4. Token Migration (Refactor Path)

Use this section when `AUDIT-QUALITY.md` or `AUDIT-PLAN.md` flags hardcoded values (colors, spacing, font sizes) in an existing codebase. Goal: replace every magic value with the correct semantic token without changing the visual output.

### Step 1 — Inventory
Run a search for hardcoded values before touching any file:
```bash
# Find hardcoded colors
grep -r "bg-\[#" src/ && grep -r "text-\[#" src/ && grep -r "border-\[#" src/
# Find hardcoded spacing
grep -r "p-\[" src/ && grep -r "m-\[" src/ && grep -r "gap-\[" src/
# Find inline styles
grep -r "style={{" src/
```
Add every finding as a LOW item in `AUDIT-PLAN.md` if not already listed.

### Step 2 — Map Values to Tokens
Before replacing, build a mapping table (add it as a comment block in `globals.css`):

```
/* TOKEN MIGRATION MAP
   #1A2B3C   → var(--color-primary)
   #F5F5F5   → var(--color-surface)
   24px      → var(--spacing-lg)
   rgba(0,0,0,0.1) → oklch(from var(--color-primary) l c h / 0.1)
*/
```

Never replace a hardcoded value with a token before the mapping table is complete — you risk inconsistency mid-migration.

### Step 3 — Replace File by File
Work one file at a time. For each file:
1. Replace the hardcoded value with the semantic token.
2. Visually verify in the browser before moving to the next file.
3. Mark the `AUDIT-PLAN.md` item as done.

### Step 4 — Verify
After all replacements:
- Toggle dark mode (if applicable) — every migrated element must respond correctly.
- Check for any remaining `grep` hits from Step 1.
- Run `core-quality` UI/CSS checkpoint.

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 2: BUILD (Category: **DEVELOPMENT**).
2. **Objective**: Create the technical token system (Colors, Spacing, Typography) ready for code.
3. **Recommended Next Step**:
   - If tokens are ready → Skill: `web-ux-ui` to implement components.
   - If color accessibility review is needed → Skill: `core-ux` (Phase 1: FOUNDATION).
4. **Tool Tip**: A code-specialized agent ("Builder") is ideal here for writing CSS and configuring the design system.
