---
name: core-ux
category: strategy
description: Universal user experience principles applicable to any interface — web, mobile, desktop, enterprise software. Activate this skill when designing or evaluating any interface a user interacts with. The principles here are technology-agnostic. CSS/React implementations are in web-ux-ui.
---

# UX Principles — Universal User Experience Principles

These principles apply to any interface that a person uses: a mobile app, a management system, a webapp. They don't depend on CSS, React, or any framework. Before implementing, understand what you're building.

---

## Principle 1 — Visual Hierarchy

The interface communicates importance through size, weight, and position. The user's eye must always know where to look first.

**The three questions every screen must answer in order:**
1. Where am I? (title, context, breadcrumb)
2. What can I do here? (main action clearly visible)
3. What happens next? (clear next step)

**How to create hierarchy:**
- Size: more important text is larger
- Weight: more important text is bolder
- Contrast: the main element has more contrast with the background
- Space: important things have more space around them
- Position: top-left is the natural eye starting point (Western culture)

**Anti-patterns:**
- Everything equal = nothing is important
- Too many elements highlighted simultaneously
- Primary CTA hidden at the bottom of the page

---

## Principle 2 — Consistent Spacing (The Spacing Law)

White space is not empty space — it's structure. Spacing communicates the relationship between elements: close = related, distant = separate.

**The rules:**
- Use a fixed spacing scale (e.g., 4, 8, 12, 16, 24, 32, 48, 64px). Never random values (13px, 7px, 23px)
- Internal spacing (padding) must be proportional to content size
- Spacing between related groups is smaller than spacing between different sections
- Nothing bumping into edges — every interface has consistent margins/padding

**Space hierarchy:**
```
Page margin (largest)
  └─ Space between sections
       └─ Space between related components
            └─ Component internal padding (smallest)
```

**If spacing feels wrong** but you can't tell why: you're probably mixing different scales. Go back to a multiple of 4 or 8.

---

## Principle 3 — Readability First

Text is the most-used part of any interface. If it doesn't read well, everything else loses value.

**Line length:** 60-75 characters for body text. Longer lines tire the eye. Shorter lines break the rhythm too much.

**Minimum contrast:** 4.5:1 between text and background for normal text (WCAG AA). 3:1 for large text (≥18px or ≥14px bold). Don't use light grey on white for text that needs to be read.

**Minimum size:** never below 14px for readable text. 16px for body text is the safe starting point.

**Line height:** 1.4-1.6 for body text. Less suffocates, more disperses.

**Font mixing:** maximum 2 fonts per project. One for headings (can have character), one for body text (must be neutral and readable).

---

## Principle 4 — Immediate Feedback

The user must always know what's happening. A silent interface is an interface that generates anxiety.

**The three states to always communicate:**
- **Loading:** something is happening (spinner, skeleton, progress bar)
- **Success:** the action completed successfully (message, state change, animation)
- **Error:** something went wrong (clear message, not a technical error code)

**Response times:**
- < 100ms: response feels instant, no feedback needed
- 100ms–1s: show a subtle loader
- > 1s: show a visible loader with option to cancel if > 10s

**Error messages must:**
- Say what happened (not "Error 500")
- Say what to do to fix it
- Not blame the user

```
❌ "Authentication error (401)"
✅ "The credentials are incorrect. Check email and password."

❌ "Unable to complete the operation"
✅ "We can't save the changes. Check your connection and try again."
```

---

## Principle 5 — One Primary Action per Screen

Every screen or interface state has **one** primary action. The user must not choose between equivalent options.

**Primary CTA:** one only, visually dominant.
**Secondary CTAs:** support the primary action, less prominent.
**Destructive actions** (delete, archive, cancel): physically separated, with distinct color, with confirmation before execution.

```
✅ [Save changes]  [Cancel]
   ^ primary        ^ secondary, less visible

✅ [Publish article]
   Link: "Save as draft"  Link: "Delete"
   ^ main action           ^ secondary, less visual weight
```

---

## Principle 6 — Prevent Errors, Not Just Handle Them

The best error message is the one that never appears because the error was made impossible.

**Prevention techniques:**
- Real-time validation (not just on form submit)
- Disable buttons when an action is unavailable (with tooltip explaining why)
- Show requirements before the user makes a mistake (e.g., password requirements visible before typing)
- Confirmation before irreversible destructive actions
- Undo where possible instead of confirmation (less flow interruption)

**Form design:**
- Labels always visible, not just as placeholders (which disappear when typing)
- Error message near the field that caused it, not at the top of the page
- Don't reset the form on error — the user already typed that information

---

## Principle 7 — Consistency

The user learns how the interface works from the first interaction. If you change the behavior of a similar element in a different context, it confuses them.

**What must always be the same:**
- The same type of action uses the same type of control (always button, or always link — not mixed)
- Icons always mean the same thing everywhere in the app
- The tone of messages (formal, informal, technical) is consistent throughout the app
- The positions of recurring elements (navigation, actions) don't change between screens
- **Heading capitalisation**: one convention is chosen in `[ID]-BRAND.md` (Title Case, Sentence case, or ALL CAPS) and applied to every heading, label, button, and nav item across the entire interface — no mixing. If no brand brief exists yet, AI chooses based on tone and records it before writing any UI text.

**External consistency:** when possible, follow the conventions of the target platform. On mobile, the back button is top-left. On the web, the logo top-left goes to home. Don't reinvent where it's not needed.

---

## Principle 8 — Basic Accessibility

Accessibility is not an optional feature — it's the minimum to avoid excluding people.

**The bare minimum:**
- Every informational image has descriptive alternative text
- Every button and link has readable text or an accessible label
- Keyboard navigation works (Tab follows visual order, Enter activates)
- Text/background contrast meets the minimum (4.5:1 for normal text)
- Forms have labels associated with every field

**You don't need to become an accessibility expert** to respect these points. They are the 20% of effort that solves 80% of accessibility problems.

---

## How to Apply in an Audit

When analyzing an existing interface, verify in order:

1. **Hierarchy:** is it clear what to do on every screen? Is there a single primary action?
2. **Spacing:** are margins consistent? Is there breathing room between elements?
3. **Readability:** is the text readable? Is the contrast sufficient? Are lines too long?
4. **Feedback:** does the app communicate loading/success/error? Are error messages clear?
5. **Consistency:** do similar elements behave the same way? Are icons consistent?
6. **Accessibility:** can you navigate with a keyboard? Do images have alt text?

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 1: FOUNDATION (Category: **STRATEGY**).
2. **Objective**: Establish usability, hierarchy, and accessibility principles before development begins.
3. **Recommended Next Step**:
   - If UX principles are clear → Skill: `web-ux-ui` or `web-design-tokens` (Phase 2: BUILD).
4. **Tool Tip**: A "Strategist" agent (Chat AI) is ideal for discussing user flows and visual hierarchy without getting lost in code.
