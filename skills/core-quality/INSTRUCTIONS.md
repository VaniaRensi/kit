---
name: security-quality
category: QUALITÀ
description: Security, code quality, testing, and performance checklist to run at project checkpoints. Use this skill when the user approves a checkpoint (planned or improvised), or when they explicitly ask "check security", "clean up the code", "do a review". Do not run these checks continuously — only at confirmed checkpoints.
---

# Security & Quality — Checkpoint Checklist

This skill runs at confirmed checkpoints, not continuously. Execute the sections in the order shown, report problems found, and propose corrections before proceeding.

4.  **Checkpoint Report**: At the end of the review, you MUST provide a standardized table. Do not skip categories. If no issues were found, mark as ✅.

### 🏁 Checkpoint Summary: [Milestone Name]
| Category | Status | Notes / Fixes Made |
|----------|--------|-------------------|
| **Security** | ✅/❌ | RLS, Env vars, Sanitization |
| **Code Quality** | ✅/❌ | TS types, clean imports, naming |
| **Performance** | ✅/❌ | Optimistic UI, bundle size |
| **UI / CSS** | ✅/❌ | Tokens used, responsiveness, hover states |
| **Context Specific** | ✅/❌ | Proactively find issues unique to THIS project |

**🚨 Proactive Audit**: Oltre alle categorie standard, DEVI analizzare il progetto per identificare rischi o debiti tecnici specifici che non sono elencati sopra. Non limitarti a una lista passiva.

---

## How to Run a Checkpoint

1. Read all code involved in the milestone or block being verified
2. Execute sections in order: Security → Quality → Testing → Performance → Git
3. For each problem found: describe the problem, explain why it's a risk, propose the solution
4. After correction, update `PROJECT-STATUS.md` and mark the area as STABLE

---

## 1. Security

### Input and User Data
- No user input is used directly in queries, commands, or HTML without sanitization
- Sensitive environment variables (API keys, secrets) are in `.env` and not in code
- The `.env` file is in `.gitignore`
- No hardcoded credentials in source code

### Authentication and Authorization
- Protected routes actually verify authentication before responding
- Session tokens have expiration
- Sensitive actions (deletion, payment, modifying others' data) verify permissions too, not just authentication
- Passwords are never stored in plaintext

### API and Communication
- Frontend API calls don't expose secrets
- Server-side APIs validate received data (don't trust the client)
- CORS is configured restrictively, not open to `*` in production

### Database
- Queries use prepared parameters or ORM — no string concatenation to build queries
- Database access policies are defined (row-level security if using Supabase)

---

## 2. Code Quality

### Structure
- Every component/function does one thing only (single responsibility principle)
- No function exceeds ~50 lines — if longer, it needs to be split
- No business logic in presentation components
- Variable and function names describe what they do, not how they do it

### Error Handling
- Every async call (fetch, DB query, file operation) has an error handling block
- Errors show a useful message to the user, not a stack trace
- Edge cases are handled: empty data, empty arrays, null/undefined values

### Readability
- No commented-out code left lying around — if it's not needed, remove it
- Comments explain the why, not the what (the what is readable from the code)
- No variables named `temp`, `data2`, `test`, `thing`

### Dependencies
- No unused imports
- No installed but unused dependencies
- Versions of critical dependencies are pinned (no `*` or overly broad ranges)

---

## 3. Testing

### Minimum Acceptable
- Every function containing logic (calculations, transformations, validations) has at least one test
- Critical flows (authentication, payments, data saving) have tests covering both the happy path and errors
- Tests must run without manual configuration

### What to Test First
1. Authentication and authorization logic
2. Data calculations and transformations
3. Input validation
4. Integration with external services (with appropriate mocks)

### What Not to Obsess Over Testing
- Purely visual components without logic
- Thin wrappers around external libraries
- Code that could never fail (simple getters, constants)

---

## 4. Performance (Basic Check)

- Images have appropriate dimensions — no 3MB images for an icon
- Data is loaded when needed (lazy loading), not all at startup
- No duplicate API calls for the same data in the same session
- Long lists use virtualization or pagination
- JavaScript bundles don't contain huge libraries imported entirely when only small parts are needed

---

## 5. Git — Conventions

### Commit Structure
Use the Conventional Commits format:
```
type(scope): short description in English

Author: [name of who did the work]
Reason: [why this change was made]
```

**Types:**
- `feat` — new feature
- `fix` — bug fix
- `refactor` — code change without changing functionality
- `test` — adding or modifying tests
- `chore` — dependency updates, configuration
- `docs` — documentation only

**Examples:**
```
feat(auth): add Google OAuth login

Author: Vania
Reason: needed for passwordless user onboarding
```

### Automatic Commit Message Generation

At every checkpoint, **don't just remind to commit** — always propose the complete message, ready to use, in this format:

```
📝 Suggested commit message:

git commit -m "feat(dashboard): complete live data visualization

Author: [current user name]
Reason: dashboard milestone completed and verified at checkpoint"
```

The user copies, pastes, and changes only their name if needed. Zero effort.

If the change involves the **shared base skills** (the `ai-kit-base/` folder), add the `[SKILL-BASE]` tag to the commit and explicitly flag it:

```
📝 Suggested commit message (skill base change — affects all team projects):

git commit -m "fix(skill-base/security): add CORS check for production [SKILL-BASE]

Author: [name]
Reason: missing CORS validation for multi-domain environments
Impact: applies to all future projects"
```

### When to Commit
Commit frequently to create "Save Points." Don't wait for the end of the day.

- **Atomic Commits**: Commit one logical change at a time (e.g., "Add login button", then "Fix login validation").
- **After every Checkpoint**: Once an area is marked as STABLE, commit it immediately.
- **After major fixes**: If you spent 30 minutes fixing a bug, commit it once it works.
- **Before major refactors**: Save the current state before you start changing everything.
- **🚨 COMMIT AUTHORIZATION**: Prima di eseguire qualsiasi comando di `git commit` o `git push`, devi fermarti e chiedere esplicitamente: *"Ho completato [task/checkpoint], posso procedere con il commit e il push?"*. Non dare mai per scontato che l'utente voglia pushare immediatamente, specialmente se il push attiva un deploy automatico (Vercel/Netlify).
- **Never** commit code that doesn't build or has red tests.

### When to Push to GitHub
Pushing moves your "Save Points" to the cloud. Do it to prevent data loss.

- **After every Milestone**: When a major feature is finished and committed, push to the remote.
- **End of Session (MANDATORY)**: Before finishing work for the day, push all your commits to GitHub.
- **Before switching agents**: If you are transitioning from Architect to Coder, push the state so the new agent can pull the latest changes.
- **Syncing**: If you are working in a team, pull before you start and push after you finish.

---

## Reporting Results

After running the checkpoint, report as follows:

```
## Checkpoint Results — [milestone/area name]

✅ Security: OK
⚠️ Quality: 2 problems found and fixed
   - [problem 1 description] → [solution applied]
   - [problem 2 description] → [solution applied]
✅ Testing: minimum coverage present
✅ Performance: no relevant issues
✅ Git: commit ready (see below)

## 🏁 Percorso Skills & Prossimo Passo

1. **Stato Attuale**: FASE 3: CONTROLLO (Categoria: **QUALITÀ**).
2. **Obiettivo**: Consolidare il codice e marcare l'area come STABLE.
3. **Prossimo Passo Consigliato**:
   - Se il codice è STABLE -> Skill: `core-documentation` o SEO (Fase 4: LANCIO).
   - Se serve un altro ciclo di sviluppo -> Skill: `web-ux-ui` (Fase 2: SVILUPPO).
4. **Tool Tip**: Un agente specializzato in "Audit" (come Claude Code) è perfetto per questa fase di pulizia profonda.
```
