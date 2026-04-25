---
name: historification
category: AGNOSTICO
description: Maintaining a decision log and local snapshots of the project.
---

# Historification Protocol

This skill ensures that the project has a memory. It prevents "circular engineering" (trying something that was already tried and failed) and provides insurance against destructive changes.

## 1. The Decision Log (`HISTORIFICATION.md`)

When a major architectural decision is made, create or update `HISTORIFICATION.md` in the root directory.

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

## 🏁 Percorso Skills & Prossimo Passo

1. **Stato Attuale**: Trasversale (Categoria: **AGNOSTICO**).
2. **Obiettivo**: Garantire la persistenza delle decisioni e dei "punti di ripristino" del progetto.
3. **Prossimo Passo Consigliato**:
   - Se hai salvato uno snapshot -> Continua con la Fase corrente (SVILUPPO o QUALITÀ).
4. **Tool Tip**: Qualsiasi agente può (e deve) historificare, ma uno Strategist è migliore nel documentare il "perché" delle scelte.
