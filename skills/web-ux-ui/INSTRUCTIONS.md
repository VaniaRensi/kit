---
name: web-ux-ui
category: development
description: Professional web interface patterns using Tailwind, accessible primitives, and consistent layout systems.
---

# Web UX & UI — Component Implementation

Use this skill to build professional, accessible, and high-performance web interfaces using React/Next.js and Tailwind CSS.

## 1. Pattern-Driven Development
Do NOT build ad-hoc components. Use established patterns:
- **Sections**: Use the standard `section > div.container` pattern.
- **Grids**: Use 12-column grids for complex layouts or auto-filling grids for lists.
- **Cards**: Use semantic tokens for padding (`p-card`) and surface colors.

## 2. Accessible Primitives
Ensure all interactive elements (buttons, links, inputs) have:
- Clear hover, focus, and active states.
- High contrast (refer to `core-ux` if unsure).
- Proper ARIA labels if icons are used without text.

## 3. Implementation Workflow

1.  **Draft Structure**: Build the semantic HTML/JSX structure first.
2.  **Instant Feedback (Optimistic UI)**: For interactive lists (Tasks, Routines), implement optimistic updates. User actions should be reflected in the UI immediately without waiting for server confirmation (using `useOptimistic` or similar patterns).
3.  **Debug Mode (Mandatory)**: During development, implement a visible debug layer or log console (usually at the bottom of the page) that captures API errors and state changes. Never let an error fail silently.
4.  **Admin Area (/admin)**: Every app MUST include a protected `/admin` route. This area must provide:
    - User Management (view/edit subscribers).
    - Settings Management (plans, feature flags, global constants).
    - Database Health check.
    - Suffix the logic based on the Strategy defined in PHASE 1.
4.  **Apply Tokens**: Style using only framework tokens from `globals.css`.

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 2: BUILD (Category: **DEVELOPMENT**).
2. **Objective**: Implement professional, accessible, and high-performance web interfaces.
3. **Recommended Next Step**:
   - If the UI is ready → Skill: `core-quality` for quality control (Phase 3: CONTROL).
   - If a UX review is needed → Skill: `core-ux` (Phase 1: FOUNDATION).
4. **Tool Tip**: A code-specialized agent ("Builder") is essential here to handle component and styling complexity.
