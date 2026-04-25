---
name: core-naming
category: QUALITÀ
description: Universal code naming principles. Activate this skill at the start of every project and whenever establishing a naming convention. Governs how variables, functions, classes, files, and folders are named — regardless of language.
---

# Naming Conventions — How Things Are Named

Names in code are the first form of documentation. A good name makes code readable without explanation. A bad name forces you to read the implementation to understand what it does.

---

## Core Rule — English First

**Everything related to code is written in English:**
- Variable, function, class, and module names
- File and folder names
- Table and column names in the database
- Technical comments in code

**Why:** English code is universal — any developer can read it, any AI can process it, any international documentation understands it. Non-English code creates an invisible barrier that you pay for when someone new arrives or when you seek help online.

---

## Descriptive Names, Not Abbreviated

The name must say **what it does** or **what it represents**, not how it's implemented or how long it takes to type.

```
❌ usr, tmp, d, fn, cb, mgr, util
✅ currentUser, temporaryFile, createdAt, formatDate, onSuccess, userManager

❌ getUsr()
✅ getUserById()

❌ lst
✅ activeSubscriptions

❌ handleClick()   (what click? where does it go?)
✅ handleAddToCart()
```

**Acceptable exceptions:**
- `i`, `j`, `k` in simple loops
- `e` for the error in catch blocks
- `el` or `node` for generic DOM references

---

## Conventions by Type

Every type of entity has its own convention — the shape of the name already tells you what you're looking at.

### Variables and Constants

```
// Variable: camelCase, noun or noun + adjective
let userEmail = "..."
let isLoggedIn = false
let totalPrice = 0
let activeFilters = []

// Configuration constant: UPPER_SNAKE_CASE
const MAX_RETRY_ATTEMPTS = 3
const API_BASE_URL = "https://..."
const DEFAULT_TIMEOUT_MS = 5000
```

### Functions and Methods

```
// Function: camelCase, starts with a verb
function getUserById(id) { }
function calculateTotalPrice(items) { }
function validateEmailFormat(email) { }
function formatDateToISO(date) { }

// Boolean functions: is / has / can / should
function isEmailValid(email) { }
function hasPermission(user, action) { }
function canEditPost(user, post) { }
```

### Classes and Interfaces

```
// Class: PascalCase, singular noun
class UserRepository { }
class PaymentService { }
class EmailNotifier { }
class OrderProcessor { }

// Interface (in typed languages): PascalCase, often with I prefix or descriptive suffix
interface IUserRepository { }   // C#/Java style
interface UserRepository { }    // modern TypeScript style
```

### Files and Folders

```
// File containing a class or component: PascalCase
UserCard.tsx
PaymentService.ts
OrderRepository.java

// File with utility functions, hooks, config: camelCase or kebab-case
formatDate.ts
useAuthentication.ts
api-client.ts
tailwind.config.js

// Folders: kebab-case
user-management/
design-system/
api-endpoints/
```

---

## Booleans: Always a Yes/No Question

A boolean name must sound like a question answered by yes or no.

```
❌ loading, status, active, visible
✅ isLoading, isActive, isVisible

❌ userLogged, formValid
✅ isUserLoggedIn, isFormValid

❌ error (could be string, object, boolean...)
✅ hasError (boolean), errorMessage (string), validationErrors (array)
```

---

## Event Handlers: on + event + context

```
❌ click(), submit(), change()
✅ onButtonClick(), onFormSubmit(), onInputChange()
✅ handleAddToCart(), handleUserLogin(), handleModalClose()
```

---

## No Magic Numbers

Hardcoded numeric values in code say nothing. They become named constants.

```
❌ if (password.length < 8)
✅ const MIN_PASSWORD_LENGTH = 8
   if (password.length < MIN_PASSWORD_LENGTH)

❌ setTimeout(callback, 3000)
✅ const DEBOUNCE_DELAY_MS = 3000
   setTimeout(callback, DEBOUNCE_DELAY_MS)

❌ if (user.role === 2)
✅ const ROLE_ADMIN = 2
   if (user.role === ROLE_ADMIN)
   // or even better: enum Role { Admin = 2 }
```

---

## Database Conventions

The same rules apply to tables, columns, and queries:

```
// Tables: snake_case, plural noun
users
order_items
payment_transactions

// Columns: snake_case
user_id
created_at
is_verified
email_confirmed_at

// Foreign keys: table_name_id
user_id (FK to users)
order_id (FK to orders)
```

---

## Signals That Naming Needs Review

During a checkpoint or review, look for these anti-patterns:

- Single-letter names outside loops (`d`, `x`, `a`)
- Opaque abbreviations (`mgr`, `proc`, `svc`, `tmp`)
- Empty generic names (`data`, `info`, `stuff`, `thing`, `object`, `list`)
- Numbers in names (`button2`, `function3`, `data_new`)
- Names that lie: a function called `getUser` that also modifies data
- `Manager` suffix without a clear boundary (often indicates a class doing too many things)

---

## 🏁 Percorso Skills & Prossimo Passo

1. **Stato Attuale**: FASE 3: CONTROLLO (Categoria: **QUALITÀ**).
2. **Obiettivo**: Garantire leggibilità e manutenibilità attraverso nomi chiari e professionali.
3. **Prossimo Passo Consigliato**:
   - Se il naming è verificato -> Skill: `core-quality` per checkpoint finale.
   - Se serve documentare -> Skill: `core-documentation` (Fase 4: LANCIO).
4. **Tool Tip**: Un agente specializzato in "Audit" (QUALITÀ) è il più adatto per rilevare nomi ambigui o non conformi.
