# 🚀 AI KIT BASE — Installation Guide

This kit is designed to be a portable "intelligence engine" (Nugget) for your software projects. You can include it as a Git Submodule or simply copy the `kit/` folder into your repository.

## 1. Fast Integration
Copy the `kit/` folder into the root of your project:
```bash
your-project/
├── kit/               <-- The Engine
├── src/
├── package.json
└── ...
```

## 2. Activation (The First Prompt)
To activate the kit, point your AI Agent (Claude Code, Cursor, ChatGPT, etc.) to the entry point. Copy and paste this as your first message:

> "I want to use the AI Kit Base for this project. Please read `kit/PROMPT.md` and follow the instructions to initialize the project status and workflow."

## 3. Maintenance
- **Read-Only**: In your implementation projects, treat the `kit/` folder as read-only. 
- **Upstream Updates**: To get new skills or improvements, update the `kit/` folder from the main [AI Kit Base repository](https://github.com/vaniarensi/ai-kit-base).
- **Project Memory**: The kit will create `[ID]-STATUS.md` and `[ID]-HISTORY.md` in your project root. These files are YOUR project's memory; keep them!

---
*Build faster. Build better. Follow the Golden Path.*
