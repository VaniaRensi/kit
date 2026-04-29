---
name: brand-discovery
category: strategy
description: Guides the strategic discovery phase before any design or frontend work. Activate this skill when starting a project with a user interface, before writing any visual code. Covers two paths: client with an existing brand (collecting logo, colors, fonts, voice) and project without a brand (proposing stylistic directions based on industry and audience). Produces BRAND-BRIEF.md which feeds into design-tokens and ux-ui-kit.
---

# Brand Discovery — Strategic Pre-Design Phase

Complete this phase before writing any CSS, tokens, or visual components. Without this information, design is guesswork.

You don't need to be creative here — you need to collect the right information in the right way.

---

## How to Start

Ask the user this question:

> "Before we start on design, I need some information. Does the client already have a defined brand (logo, colors, fonts) or are we starting from scratch?"

Based on the answer, follow **Path A** or **Path B**.

---

## Proactive Inquiry & No-Guessing Protocol

**MANDATORY RULES:**
1.  **Audience First, Colors Last**: You are FORBIDDEN from discussing specific colors, hex codes, or fonts until the **Target Persona** and **Emotional Goal** (the "feeling") are documented and approved.
2.  **The "Programmer-Short" Rule**: If a user provides brief, one-word, or insufficient answers (typical of busy developers), do NOT proceed. You must acknowledge the input and ask specific, high-context follow-up questions to dig deeper into the "Why" and the "Feeling".
3.  **No Hallucinated Preferences**: Never assume a "standard" style for an industry. Every brand must be built from the user's specific vision. If the vision is missing, keep inquiring.
4.  **One Step at a Time**: Never ask for the objective, platform, and colors in the same message. This causes cognitive overload and leads to shallow decisions.

---

---

## Path A — Existing Brand

Collect the client's brand information. Ask questions in this order, one at a time (don't dump everything at once).

### A1. Visual Identity
- "Do you have a logo? Feel free to upload it — I'll analyze it to extract the dominant colors."
  - If uploaded: analyze the logo and propose extracted colors as a starting point
  - If not available: ask for hex values directly
- "What are the official brand colors?"
  - Primary color (main actions, CTAs)
  - Secondary color (support, less prominent accents)
  - Accent color (highlights, notifications, distinctive elements)
  - Confirm: do these colors have light/dark variants? Do they already exist?

### A2. Typography
- "What fonts does the brand use?"
  - Heading font
  - Body text font
  - If unknown: "Do you have an existing website or materials we can extract it from?"
  - If missing: propose 2-3 font pairings compatible with the brand style (see section B3 for selection logic)
- "Are the fonts Google Fonts, local files, or purchased?"

### A3. Voice and Tone
- "How does this brand communicate? Choose the closest:"
  - Professional and authoritative
  - Friendly and accessible
  - Energetic and direct
  - Calm and reassuring
  - Sophisticated and premium
  - Other (describe)
- "Are there phrases or words the brand uses often? Or wants to avoid?"

### A4. Audience
- "Who is the primary target?"
  - Average age (e.g., 25-40)
  - Profession or context (e.g., professionals, parents, students)
  - What are they looking for when they use this product?
  - Is it B2B (businesses) or B2C (consumers)?

### A5. Visual Style References
- "Do you have examples of sites or apps you like for their style? (even competitors, even outside the sector)"
- "Is there a style to absolutely avoid?"

---

## Path B — Brand to Build

When there's no existing brand, the AI proposes strategic directions based on the project. Don't invent — reason from the project information.

### B1. Basic Information Collection
- "What sector does this product operate in?"
  - E.g., fintech, wellness, B2B SaaS, e-commerce, education, food, etc.
- "Who is the target?"
  - Age, profession, usage context
  - B2B or B2C?
- "What feeling should the interface convey?"
  - Trust and security
  - Energy and dynamism
  - Calm and clarity
  - Exclusivity and premium
  - Accessibility and simplicity

### B2. Stylistic Research
Before proposing, use the `ux-ui-kit/ui-ux-pro-max` skill to search:
```
python3 ai-kit-base/ux-ui-kit/ui-ux-pro-max/scripts/search.py "[industry] [tone] [audience]" --design-system
```
This returns: recommended style, color palette, font pairings, anti-patterns to avoid for that type of product.

### B3. Propose 2-3 Stylistic Directions
Present options in this format for each:

```
DIRECTION [N]: [Direction Name]
Style: [e.g., Minimal Clean / Bold Modern / Soft Warm]
Colors: primary #XXXXXX · secondary #XXXXXX · accent #XXXXXX
Fonts: [Heading font] + [Body font] — [reason for choice in 1 line]
Suitable because: [2 lines connecting the choice to the industry and audience]
```

Briefly explain the reasoning behind each choice — don't propose at random, but with precise reasoning.

### B4. Choice and Confirmation
- The user chooses a direction or requests modifications
- You can mix elements from different directions if requested
- Once the choice is confirmed, proceed to creating the BRAND-BRIEF

---

## Output: BRAND-BRIEF.md

At the end of both paths, create the `BRAND-BRIEF.md` file in the project folder.

```markdown
# Brand Brief — [Project Name]

> Created: [date] | Updated: [date]

## Visual Identity

### Colors
| Role | Hex | OKLCH | Usage |
|------|-----|-------|-------|
| Primary | #XXXXXX | oklch(...) | Main CTAs, interactive elements |
| Secondary | #XXXXXX | oklch(...) | Support, section backgrounds |
| Accent | #XXXXXX | oklch(...) | Highlights, badges, distinctive elements |
| Text | #XXXXXX | oklch(...) | Main body text |
| Background | #XXXXXX | oklch(...) | Page background |
| Surface | #XXXXXX | oklch(...) | Cards, panels, components |

### Typography
| Role | Font | Weight | Notes |
|------|------|--------|-------|
| Headings | [font] | 700 | [origin: Google/file/system] |
| Body | [font] | 400 | [origin] |
| Interface | [font or same as body] | 500 | Labels, buttons |

### Visual Style
- Style: [e.g., Minimal / Glass / Bold / Soft]
- Border radius: [e.g., rounded / sharp / mixed]
- Shadows: [e.g., light / none / pronounced]
- Dark mode planned: [yes / no / future]

## Strategy

### Voice and Tone
- Tone: [e.g., professional but accessible]
- Brand keywords: [list]
- Words to avoid: [list]

### Audience
- Primary target: [description]
- B2B / B2C: [specify]
- Usage context: [e.g., desktop at work / mobile on the go]

### Sector and Competition
- Sector: [industry]
- Positive style references: [links or names]
- Styles to avoid: [reason]

## Notes
[Decisions made, trade-offs, things to revisit]
```

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 1: FOUNDATION (Category: **STRATEGY**).
2. **Objective**: Stabilize the `[ID]-BRAND.md`.
3. **Recommended Next Step**:
   - If the Brand is stable → Skill: `web-design-tokens` (Phase 2: BUILD).
   - If technical architecture needs to be defined → Skill: `core-architecture` (Phase 1: FOUNDATION).
4. **Tool Tip**: When transitioning to Phase 2 (BUILD), consider switching to an agent specialized in code (e.g., Claude Code, Cursor) to maximize efficiency.
