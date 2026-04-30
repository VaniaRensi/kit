---
name: web-ux-ui
category: development
description: Professional web interface patterns using Tailwind, accessible primitives, and consistent layout systems.
---

# Web UX & UI — Component Implementation

Use this skill to build professional, accessible, and high-performance web interfaces using React/Next.js and Tailwind CSS.

## 1. Layout System — Grid First

**Grid is the default for all layout containers. Flexbox is for component internals and single-axis alignment.**

| Use Grid for | Use Flexbox for |
|---|---|
| Page sections and structure | Inside a card (stacking title → content → button) |
| Card grids and tile layouts | Navigation bars and tab lists |
| Any layout needing row AND column alignment | Centering a single element |
| Equal-height rows | Button groups aligned on one axis |

Never reach for Flexbox to build a multi-column layout. Grid handles two dimensions; Flexbox handles one.

### Equal-Height Cards with Pinned CTAs

This is the standard pattern for any card grid. Cards in the same row are always the same height. The CTA is always at the bottom, regardless of how much content each card contains.

```jsx
{/* Grid container — equal height rows automatic */}
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  <CardComponent />
  <CardComponent />
  <CardComponent />
</div>

{/* Card — flex column so CTA pins to bottom */}
<div className="flex flex-col p-card bg-surface rounded-lg">
  <h3 className="text-heading">Card Title</h3>
  <p className="flex-1 mt-2 text-body">           {/* flex-1 stretches to fill space */}
    Card description — can be short or long,
    the button will always stay at the bottom.
  </p>
  <a href="#" className="mt-auto btn-primary">    {/* mt-auto pins to bottom */}
    Call to Action
  </a>
</div>
```

**Why this works:**
- `grid` makes all cards in the same row equal height automatically
- `flex flex-col` on the card makes the internal layout a vertical stack
- `flex-1` on the content area stretches it to fill the available space
- `mt-auto` on the CTA pushes it to the bottom regardless of content length

### Title Alignment Across Cards

If card titles can be different lengths (one line vs two lines), use CSS subgrid or a `min-height` on the title element to keep them baseline-aligned across the row:

```jsx
{/* Option A — min-height on title (simpler, works everywhere) */}
<h3 className="min-h-[3rem] text-heading">Card Title</h3>

{/* Option B — CSS subgrid (cleanest, modern browsers) */}
<div className="grid grid-cols-3 gap-6 [&>*]:grid [&>*]:grid-rows-subgrid [&>*]:row-span-3">
  {cards.map(card => (
    <div key={card.id}>        {/* row 1: title */}
      <h3>{card.title}</h3>    {/* row 2: content */}
      <p>{card.body}</p>       {/* row 3: CTA */}
      <a href={card.href}>CTA</a>
    </div>
  ))}
</div>
```

### Sections Pattern
```jsx
<section>
  <div className="container mx-auto px-4">
    {/* content */}
  </div>
</section>
```

- **Cards**: use semantic tokens for padding (`p-card`) and surface colors.

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
   - When creating each new page → Load `web-seo` to set metadata, images, and internal links before moving on.
   - If the UI is ready → Load `core-quality` for quality control (Phase 3: CONTROL).
   - If a UX review is needed → Load `core-ux` (Phase 1: FOUNDATION).
4. **Tool Tip**: A code-specialized agent ("Builder") is essential here to handle component and styling complexity.
