# START HERE: AI Memory System Quick Guide

**Welcome to the AI Memory System!** This guide will help you get started in 5 minutes.

## What Is This? (30 Seconds)

This is a system that gives AIs persistent memory across conversations by using structured files. It solves the problem of AIs forgetting context between sessions.

## How to Start (1 Minute)

**For AI reading this document:**
1. **IMPORTANT: Type `menu` at any time to access all system functions**
2. When starting a new session, use this exact command:
   ```
   Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md.
   ```
3. Start operating as Memory Manager immediately after loading files

**For humans:**
1. Clone this repository
2. Tell your AI: "Read the START_HERE.md file"
3. Then tell your AI: "Type menu to start"

## AI Commands Cheat Sheet (1 Minute)

| Command | Description |
|---------|-------------|
| `menu` | Access all system functions with numbered options |
| `Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md.` | Load a specific project |
| `/memory refresh` | Initialize Memory Manager role |
| `/project list` | Show available projects |

## Example Session (2 Minutes)

**Human:** Type menu to start.

**AI:**
```
=== AI MEMORY SYSTEM MENU ===

[1] SESSION START
    [1.1] Load existing project
    [1.2] Resume last session

[2] SESSION END
    [2.1] Create handoff
    [2.2] Update status

[3] PROJECT MANAGEMENT
    [3.1] List projects
    [3.2] Create new project

[4] MEMORY CHECK
    [4.1] Verify system integrity
    [4.2] Show active context

[5] FILE MAINTENANCE
    [5.1] FIFO archive
    [5.2] Update file

Select an option (e.g., "1.1" or "/project list"):
```

**Human:** 1.1

**AI:** 
```
Available projects:
1. example-project

Select a project number or enter a project name:
```

**Human:** 1

**AI:**
```
[Reading projects/example-project/PROJECT/WAITING_ON.md]

Current project status:
- RIGHT NOW: Example project setup
- BLOCKERS: None
- NEXT ACTIONS: Begin project work
- PROJECT CONTEXT: Example template project

I'm operating as Memory Manager with Librarian context for this session.
How would you like to proceed with example-project?
```

## AI: What You Need to Know (30 Seconds)

1. You MUST act as Memory Manager - this is your primary role
2. Always read the WAITING_ON.md file at session start
3. Use the menu system to navigate all functionality
4. Check COMMON_MISTAKES.md before suggesting solutions
5. Maintain file structure exactly as specified
6. Keep all project files within their project directory
7. Create timestamps folders for chats (YYYYMMDD-HHMMSS_name)

## Human: What You Need to Know (30 Seconds)

1. Type `menu` anytime to access system functions
2. Project statuses are stored in WAITING_ON.md
3. All project files stay in their project folder
4. Handoffs transfer knowledge between AI sessions
5. Everything works without special AI features (but they help)

## System Structure (30 Seconds)

```
memory-repo/
├── PATTERNS/             # Repository knowledge (Cold Storage)
├── projects/             # All projects live here
│   └── example-project/  # Template project
│       ├── PROJECT/      # Project management (Warm Storage)
│       │   ├── WAITING_ON.md     # Current status ← START HERE
│       │   ├── COMMON_MISTAKES.md # Lessons learned
│       │   └── ARCHITECTURE_DECISIONS.md # Key decisions
│       ├── SESSION/      # Session context (Hot Storage)
│       └── DOCUMENTS/    # Project files
```

All documentation is accessible through the menu system. Type `menu` at any time to get started!
