---
name: web-ux-ui
category: SVILUPPO
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
2.  **Debug Mode (Mandatory)**: During development, implement a visible debug layer or log console (usually at the bottom of the page) that captures API errors and state changes. Never let an error fail silently.
3.  **Admin Area (/admin)**: Every app MUST include a protected `/admin` route. This area must provide:
    - User Management (view/edit subscribers).
    - Settings Management (plans, feature flags, global constants).
    - Database Health check.
    - Suffix the logic based on the Strategy defined in FASE 1.
4.  **Apply Tokens**: Style using only framework tokens from `globals.css`.

## 🏁 Percorso Skills & Prossimo Passo

1. **Stato Attuale**: FASE 2: COSTRUZIONE (Categoria: **SVILUPPO**).
2. **Obiettivo**: Implementare interfacce web professionali, accessibili e performanti.
3. **Prossimo Passo Consigliato**:
   - Se la UI è pronta -> Skill: `core-quality` per il controllo qualità (Fase 3: CONTROLLO).
   - Se serve una revisione UX -> Skill: `core-ux` (Fase 1: FONDAMENTA).
4. **Tool Tip**: Un agente specializzato in codice ("Builder") è fondamentale qui per gestire la complessità dei componenti e dello stile.
