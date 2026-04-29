---
name: historification
category: agnostic
description: Maintaining a decision log and local snapshots of the project.
---

# Historification Protocol

This skill ensures that the project has a memory. It prevents "circular engineering" (trying something that was already tried and failed) and provides insurance against destructive changes.

## 1. The Decision Log (`[ID]-HISTORY.md`)

When a major architectural decision is made, create or update `[ID]-HISTORY.md` in the root directory.

### Entry Structure
```markdown
### YYYY-MM-DD: [Title of Decision]

- **Context**: What was the situation? Why was a change needed?
- **The Problem**: What exactly was failing or causing friction?
- **Considerations**: What alternatives were discussed? What were the pros/cons?
- **The Decision**: What did we actually do?
- **Consequences**: What happened after? (Can be updated later)
```

## 2. The Snapshot System

Before making high-risk changes (e.g., changing colors, refactoring the layout, swapping a major library), or immediately after a successful "visual polish" session, create a snapshot.

### Snapshot Procedure
1. Create a directory: `.snapshots/YYYY-MM-DD-description/`
2. Copy the files that define the current "look and feel":
   - Global CSS files
   - Tailwind/Framework config files
   - Main page/layout files
3. Add a `note.txt` explaining why this snapshot is being taken.

### Restoring a Snapshot
If a future change breaks the UI beyond easy repair, the AI agent must consult the latest snapshot and restore the files to return to the last known-good state.

## 🏁 Skill Path & Next Step

1. **Current State**: Cross-cutting (Category: **AGNOSTIC**).
2. **Objective**: Ensure persistence of decisions and project restore points.
3. **Recommended Next Step**:
   - If you saved a snapshot → Continue with the current phase (DEVELOPMENT or QUALITY).
4. **Tool Tip**: Any agent can (and should) historify, but a Strategist is best at documenting the *why* behind decisions.
