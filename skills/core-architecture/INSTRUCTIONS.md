---
name: core-architecture
category: STRATEGIA
description: Universal code structure principles applicable to any language or platform. Activate this skill at the start of every project and whenever organizing a new feature. Governs how code is divided into pieces — not how it looks or what it does.
---

# Architecture — Code Structure

These principles apply to any project, regardless of language or platform. Clear architecture is what separates a project that grows cleanly from one that becomes unmanageable.

---

## Principle 1 — One Responsibility per Unit

Every file, function, class, or module does **one thing only**. If you need "and" to describe what a piece of code does, it should be split.

```
❌ UserManager — handles authentication AND saves to database AND sends email
✅ AuthService — handles login/logout only
✅ UserRepository — handles user persistence only
✅ EmailNotifier — handles email sending only
```

**Signals that a function does too many things:**
- Exceeds 30-50 lines
- Has more than 3 levels of nested indentation
- Its name contains "and" or "&"
- It changes for two different reasons (e.g., UI change and business logic change)

---

## Principle 2 — Separation of Presentation / Logic / Data

Three distinct layers that never mix:

```
┌─────────────────────────────────────┐
│  Presentation                       │  Displays data, collects input
│  (UI, template, view)               │  Knows nothing about the database
├─────────────────────────────────────┤
│  Business Logic                     │  Calculates, transforms, decides
│  (service, use case, controller)    │  Doesn't know how data is displayed
├─────────────────────────────────────┤
│  Data                               │  Reads, writes, persists
│  (repository, model, DAO)           │  Contains no business logic
└─────────────────────────────────────┘
```

**Common anti-patterns to avoid:**
- Database queries directly in UI components
- Calculation logic in presentation files
- Output formatting in business logic
- Direct HTTP calls in components (without a service layer)

---

## Principle 3 — Organize by Feature, Not by Type

Group files by what they do together, not by how they're technically built.

```
❌ By type (everything gets mixed as it grows)
src/
├── components/
│   ├── UserCard.jsx
│   ├── ProductCard.jsx
│   └── OrderCard.jsx
├── services/
│   ├── userService.js
│   ├── productService.js
│   └── orderService.js

✅ By feature (everything "user" needs is together)
src/
├── user/
│   ├── UserCard.jsx
│   ├── userService.js
│   └── userRepository.js
├── product/
│   ├── ProductCard.jsx
│   ├── productService.js
│   └── productRepository.js
```

**Exceptions:** truly shared components (Button, Input, Modal) go in a `shared/` or `common/` folder — but only if used by at least 3 different features.

---

## Principle 4 — Dependencies Point Inward

Dependencies always point toward the center, never toward the edges. Business logic never depends on UI or database — it's the other way around.

```
UI → Business Logic → Data Access
```

- UI can call services
- Services know nothing about UI
- Database contains no logic — it's passive storage
- Models/entities don't import frameworks or external libraries

If you change the database, only the data layer is touched. If you change the UI, only the presentation layer is touched. Business logic stays unchanged.

---

## Principle 5 — Reasonable Sizes

Practical limits that signal when to split:

| Unit | Recommended Limit | Warning Signal |
|------|-------------------|----------------|
| Function | 30 lines | > 50 lines |
| File / module | 200 lines | > 400 lines |
| Class | 5-10 public methods | > 15 methods |
| Feature folder | 5-8 files | > 12 files |

These aren't absolute rules — there are exceptions. They're alarm bells that ask: "does this piece need to be split?"

---

## Principle 6 — No Duplication (But Not Too Soon)

If the same code appears in 2 identical places, it's tolerable. If it appears in 3 places, extract it into a shared function.

**Rule of three:** wait for the third occurrence before abstracting. Abstracting too early creates unnecessary dependencies and makes code harder to understand.

```
First time: write the logic
Second time: copy (acceptable, keep an eye on it)
Third time: extract into a shared function
```

---

## Principle 7 — Clear Entry Points

Every module/feature exposes a minimal public interface. Everything else is private.

- Expose only what other modules need
- Implementation details stay internal
- If you change the internal implementation without changing the public interface, nobody notices

This is the boundary between "module" and "spaghetti": a module with a clear interface can be rewritten without touching the rest of the system.

---

## Principle 8 — Administrative Control
Every system needs an "internal eye". You must architect the project with an **Administrative Layer** in mind from Day 1:
- **Audit Logs**: Who changed what and when?
- **User Personas**: Distinguish between `End User` and `Admin`.
- **System Settings**: Move magic numbers and business rules (e.g., subscription prices) into a configurable database table accessible via the Admin UI.

---

## How to Apply to an Existing Project

When working on already-written code:

1. **Don't rewrite everything** — identify the most critical areas (the most frequently touched, the hardest to modify)
2. **Extract gradually** — move logic into separate services without changing external behavior
3. **Test before moving** — if there are no tests, write at least one behavior test before refactoring
4. **One thing at a time** — don't mix refactoring and new features in the same commit

---

## 🏁 Percorso Skills & Prossimo Passo

1. **Stato Attuale**: FASE 1: FONDAMENTA (Categoria: **STRATEGIA**).
2. **Obiettivo**: Definire la struttura tecnica e lo stack.
3. **Prossimo Passo Consigliato**:
   - Se l'architettura è pronta -> Skill: `web-ux-ui` o `web-design-tokens` (Fase 2: SVILUPPO).
4. **Tool Tip**: Rimani in un agente "Strategist" (Chat AI) per rifinire i dettagli tecnici prima di passare al terminale.
