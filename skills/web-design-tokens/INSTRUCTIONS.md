---
name: web-design-tokens
category: SVILUPPO
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

## 🏁 Percorso Skills & Prossimo Passo

1. **Stato Attuale**: FASE 2: COSTRUZIONE (Categoria: **SVILUPPO**).
2. **Obiettivo**: Creare il sistema tecnico di token (Colori, Spazi, Tipografia) pronto per il codice.
3. **Prossimo Passo Consigliato**:
   - Se i token sono pronti -> Skill: `web-ux-ui` per implementare i componenti.
   - Se serve un controllo di accessibilità sui colori -> Skill: `core-ux` (Fase 1: FONDAMENTA).
4. **Tool Tip**: Un agente specializzato in codice ("Builder") è perfetto qui per scrivere il CSS e configurare il design system.
