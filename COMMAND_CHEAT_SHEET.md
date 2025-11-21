# Memory System Command Cheat Sheet

**Purpose:** Quick reference for all memory system commands  
**Format:** Print-friendly for desk reference

---

## Universal Access Command

| Command | Description | Example |
|---------|-------------|---------|
| `menu` | Access interactive menu (not case sensitive) | `menu` or `MENU` |

---

## Slash Commands - Main Menu

| Command | Description | Numeric Equivalent |
|---------|-------------|-------------------|
| `/menu` | Return to main menu | N/A |
| `/start` | SESSION START menu | `1` |
| `/end` | SESSION END menu | `2` |
| `/project` | PROJECT MANAGEMENT menu | `3` |
| `/doc` | DOCUMENTATION menu | `4` |
| `/file` | FILE OPERATIONS menu | `5` |
| `/status` | STATUS CHECKS menu | `6` |
| `/memory` | MEMORY CHECK menu | `7` |
| `/troubleshoot` | TROUBLESHOOTING menu | `8` |
| `/help` | HELP menu | `9` |

---

## Slash Commands - Memory Functions

| Command | Description | Usage |
|---------|-------------|-------|
| `/memory refresh` | Reload memory patterns | `Use at session start` |
| `/memory check` | Check memory integrity | `Use when validation needed` |
| `/memory patterns` | Check PATTERNS/ folder usage | `Use for pattern compliance` |
| `/memory maintenance` | Check file maintenance | `Use for FIFO verification` |
| `/memory handoff` | Verify handoff compliance | `Use when creating handoffs` |

---

## Session Operations

| Action | Command/Menu | Notes |
|--------|--------------|-------|
| Start Session | `/start load` or Menu `1.1` | Loads project memory |
| End Session | `/end` or Menu `2` | Updates and creates handoff |
| Create Handoff | `/end handoff [project-number]` or Menu `2.1` | Creates an 8-section handoff |
| Update Context | `/end context` or Menu `2.2` | Updates CURRENT_CONTEXT.md |
| Update Log | `/end log` or Menu `2.3` | Updates SESSION_LOG.md |
| Update Status | `/end waiting` or Menu `2.4` | Updates WAITING_ON.md |

---

## Project Operations

| Action | Command/Menu | Notes |
|--------|--------------|-------|
| List Projects | `/project list` or Menu `3.1` | Shows all projects |
| Create Project | `/project new` or Menu `3.2` | Creates new project |
| Check Status | `/project status` or Menu `3.3` | Gets project status |

---

## File Structure Quick Reference

```
your-repository/
├── PATTERNS/               # Cold storage (750-line limits)
│   ├── VALIDATED_APPROACHES.md
│   ├── ENFORCEMENT_PATTERNS.md
│   ├── AI_FAILURE_MODES.md
│   └── HANDOFF_TEMPLATE_STANDARD.md
├── projects/
│   └── [project-name]/
│       ├── PROJECT/        # Warm storage (500-line FIFO)
│       │   ├── WAITING_ON.md
│       │   ├── COMMON_MISTAKES.md
│       │   └── ARCHITECTURE_DECISIONS.md
│       ├── SESSION/        # Hot storage
│       │   ├── CURRENT_CONTEXT.md  (<100 lines)
│       │   ├── SESSION_LOG.md      (500-line FIFO)
│       │   ├── YYYYMMDD-HHMMSS_name/  (timestamp folders)
│       │   │   └── chat.log        (750-line target)
│       │   └── YYYYMMDD-HHMMSS_handoff.md  (handoffs)
│       ├── DOCUMENTS/
│       └── README.md
```

---

## Common File Update Patterns

| File | Update Pattern | Line Limit |
|------|----------------|------------|
| WAITING_ON.md | Add to RECENT COMPLETIONS<br>Update NEXT ACTIONS | 500 lines |
| COMMON_MISTAKES.md | Add Pattern N: [Title]<br>Include: Mistake, Fix, Why | 500 lines |
| ARCHITECTURE_DECISIONS.md | Add DECISION: [Name]<br>Include: Context, Decision, Rationale | No limit |
| SESSION_LOG.md | Add Session N entry<br>Complete all session sections | 500 lines |
| CURRENT_CONTEXT.md | Keep TLDR up to date<br>Summarize key context | <100 lines |

---

## Memory Manager Contexts

| Context | Use Case | Command |
|---------|----------|---------|
| Architect | System design work | `Operate as Memory Manager with Architect context` |
| Librarian | Information retrieval | `Operate as Memory Manager with Librarian context` |
| Archivist | File maintenance | `Operate as Memory Manager with Archivist context` |
| Handoff | Session transitions | `Operate as Memory Manager with Handoff context` |

---

## Handoff Essential Sections

1. Validation Checklist
2. Essential Files
3. Next Actions
4. Known Issues/Blockers
5. Project Context
6. Current Status
7. Key Decisions
8. Tips for Next Session

---

## Reading Order - Session Start

1. Latest handoff document (if available)
2. projects/[project]/PROJECT/WAITING_ON.md
3. projects/[project]/PROJECT/COMMON_MISTAKES.md
4. projects/[project]/SESSION/CURRENT_CONTEXT.md
5. projects/[project]/PROJECT/ARCHITECTURE_DECISIONS.md

---

## Important Notes

* Remember to refresh memory at session start: `/memory refresh`
* Type `?[number]` for details about any menu option (e.g., `?2` for details on SESSION END)
* Use timestamp format YYYYMMDD-HHMMSS for all chat folders and handoffs
* Maintain FIFO discipline: Archive when approaching line limits
* Follow the 8-section handoff template for all handoffs

---

[Print this sheet for quick reference]