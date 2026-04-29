---
name: core-documentation
category: content
description: Universal principles for code and project documentation. Activate this skill at the start of every project and when establishing a documentation strategy. Governs what to document, when, and how — without over-documenting or under-documenting.
---

# Documentation — What, When, and How to Document

Documentation has a dual problem: too little and nobody understands the code. Too much and nobody reads it. The goal is to document what the code cannot explain on its own.

---

## 🚀 Execution Workflow — Step by Step

Documentation is not freeform writing. Follow this sequence every time.

### Step 1 — Load Context (Before Writing Anything)

Read the project files that define the truth before you write a single word:

| What you're documenting | File to read first | Skill to load |
|---|---|---|
| Architecture decisions | `[ID]-ARCHITECTURE.md` | `core-architecture` |
| Brand voice and product description | `[ID]-BRAND.md` | `brand-discovery` |
| UX flows and interface decisions | `[ID]-STATUS.md` + audit reports | `core-ux` |
| Design system and token decisions | `globals.css` or token file | `web-design-tokens` |
| Audit findings summary | `AUDIT-PLAN.md` + all 6 reports | `core-audit` |
| Security posture | `AUDIT-SECURITY.md` | `core-quality` |

Never document from memory. If the source file does not exist, flag it before writing.

### Step 2 — Identify Which Documents to Produce

Every project needs a minimum set. Check what's missing:

| Document | Required | Skill Reference |
|---|---|---|
| `README.md` | Always | This skill (see template below) |
| Inline code comments | Always | This skill (see Core Principle) |
| `DECISIONS.md` | If >3 major architectural choices | `core-architecture` |
| API Reference | If the project exposes a public API | This skill (see Public Interfaces) |
| User Guide | If end-users interact with the product | `core-ux` for UX language |
| SEO meta descriptions | If it's a web product | `core-ux` §Readability |
| `AUDIT-SUMMARY.md` | If the project went through AUDIT mode | Synthesize from the 6 audit reports |

### Step 3 — Write, Section by Section

Work through the document list one file at a time. For each:
1. Draft the content based on source files (Step 1).
2. Apply the Core Principle: document the **why**, not the **what**.
3. Verify against the "What NOT to Document" list below.
4. Mark the item done in `[ID]-STATUS.md`.

### Step 4 — Final Documentation Checkpoint

Before declaring documentation STABLE, verify every item in the "During a Checkpoint" section at the bottom of this skill.

---

## The Core Principle — The Why, Not the What

Well-written code already says **what** it does. Documentation explains **why** it does it that way, or **why not** another way.

```python
# ❌ Useless — says exactly what the code already says
# Increment counter by 1
counter += 1

# ✅ Useful — explains something the code cannot say
# We increment before assigning the ID because the DB uses 1-based sequences.
# counter=0 would cause a constraint violation on the FK.
counter += 1
```

**If removing a comment wouldn't change the understanding of the code, don't write it.**

---

## What to Always Document

### 1. The Project README

Every project has a `README.md` that answers these questions, in order:

```markdown
# Project Name

What this project does in one line.

## Prerequisites
What's needed to run it (runtime, versions, system dependencies).

## Setup
The exact commands to install and run it, in order. Zero ambiguity.

## Structure
The main folders and what they contain — only the non-obvious ones.

## How to Contribute
Branch strategy, commit naming, how to open a PR.

## Architectural Decisions
The important choices and why. This section is invaluable for anyone who comes later.
```

The README is not a complete technical specification. It's a map for orientation.

### 2. Public Interfaces

Any function, method, or class that other modules use should be briefly documented:
- What it receives as input (type and meaning)
- What it returns
- When it throws exceptions or errors

```typescript
/**
 * Retrieves a user by their unique identifier.
 * Returns null if no user exists with that ID.
 * Throws AuthorizationError if the caller lacks read permissions.
 */
async function getUserById(id: string): Promise<User | null>
```

Don't document private functions — they live near the code that uses them and can be read directly.

### 3. Non-Obvious Decisions

Whenever a choice is made that a future developer might want to "fix" without understanding the reason, leave a comment.

Typical cases:
- Workaround for a bug in an external library
- Specific order of operations that looks wrong but is necessary
- Optimization that hurts readability but is needed for performance
- Limitation imposed by a business requirement, not a technical one

```javascript
// Using String comparison instead of === because the legacy API returns
// numbers as strings. Do not change to strict equality — causes silent failures.
if (statusCode == "200") { ... }
```

### 4. Contracts and Invariants

If there's something that "must always be true" for the system to work, document it near the code that depends on it.

```python
# INVARIANT: items in this list are always sorted by created_at DESC.
# The pagination cursor depends on this ordering. If you modify this,
# update the pagination logic in cursor_service.py.
recent_orders = get_orders_sorted()
```

---

## What NOT to Document

- **Obvious code**: don't comment `i += 1` or `return user`
- **Code history**: that's what git is for. Don't write "added 2024-01-15 for bug XYZ"
- **TODOs without owner and date**: they become ghosts in the code. Better to open a ticket
- **Commented-out code sections**: if it's not needed, delete it. Git tracks it
- **Structure via comments**: `// === SECTION 1 ===` indicates the file is too long

---

## The Architectural Decision Log

For long-running projects, it's worth keeping a record of important decisions. Not every choice — only those that:
- Involve a significant trade-off
- Might be questioned in the future
- Depend on a context that could change

**Minimal format (goes in README or a `DECISIONS.md` file):**

```markdown
## [Date] — Why we chose [technology/approach]

**Context:** [situation at the time of the choice]
**Decision:** [what we chose]
**Alternatives considered:** [what we rejected and why]
**Consequences:** [what changes with this choice]
```

---

## Living Documentation vs Dead Documentation

Documentation dies when it's not updated. To reduce the risk:

**Close to code = more likely to be updated**
- Inline comments are seen when the code is modified
- A README in the same folder as the code it describes is read alongside the code

**Far from code = more likely to become stale**
- External wikis, Notion, Confluence: useful for big-picture, dangerous for technical details
- Documentation separate from the repository: silently expires

**Practical rule:** if information changes every time the code is modified, keep it close to the code. If it's stable and concerns the overall vision, it can live in a separate document.

---

## During a Checkpoint

In the documentation review, verify:

- README exists and is up to date
- Public functions have a line explaining what they do and what they return
- No commented-out code left lying around
- Important architectural decisions made in this milestone are documented
- Existing comments explain the why, not the what
- No orphaned TODOs without a ticket or owner

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 4: LAUNCH (Category: **CONTENT**).
2. **Objective**: Make the project understandable and maintainable long-term.
3. **Recommended Next Step**:
   - If documentation is complete → Load `core-phases` to generate the final handover package.
   - If UX copy or SEO needs work → Load `core-ux` (Phase 4: LAUNCH).
   - If architectural decisions are undocumented → Load `core-architecture` and read before writing.
   - If brand voice is unclear → Load `brand-discovery` and read `[ID]-BRAND.md` first.
4. **Where this skill sits in the flow**:
   ```
   core-refactor → core-quality (checkpoint) → core-documentation → core-phases (handover)
   ```
5. **Tool Tip**: A Chat AI agent (not a terminal agent) is best for writing documentation — it produces cleaner prose and is more cost-effective than a coding agent for this phase.
