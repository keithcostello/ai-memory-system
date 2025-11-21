# Memory System Interactive Menu
**Type a number to select a menu option**

## 🚀 MAIN MENU

[1] SESSION START - Load project memory
[2] SESSION END - Update memory and handoff
[3] PROJECT MANAGEMENT - Create/list/manage projects
[4] DOCUMENTATION - Record mistakes/decisions
[5] FILE OPERATIONS - Read/write/list files
[6] STATUS CHECKS - View project status
[7] MEMORY CHECK - Verify memory system integrity
[8] TROUBLESHOOTING - Resolve common issues
[9] HELP - Get assistance

## SLASH COMMANDS

All menu options can also be activated using slash commands:
- `/start` - SESSION START menu
- `/end` - SESSION END menu
- `/project` - PROJECT MANAGEMENT menu
- `/doc` - DOCUMENTATION menu
- `/file` - FILE OPERATIONS menu
- `/status` - STATUS CHECKS menu
- `/memory` - MEMORY CHECK menu
- `/troubleshoot` - TROUBLESHOOTING menu
- `/help` - HELP menu

Type `?[number]` for more details about any menu option (e.g., `?2` for SESSION END details).

---

## [2] SESSION END MENU

[2.1] Create handoff
[2.2] Update SESSION/CURRENT_CONTEXT.md
[2.3] Update SESSION_LOG.md
[2.4] Update WAITING_ON.md
[2.5] Return to main menu

## SLASH COMMANDS (SESSION END)

- `/end handoff` - Create a handoff document
- `/end context` - Update CURRENT_CONTEXT.md
- `/end log` - Update SESSION_LOG.md
- `/end waiting` - Update WAITING_ON.md
- `/menu` - Return to main menu

Type `?[number]` for more details (e.g., `?2.1` for handoff details).

---

## [2.1] CREATE HANDOFF

**Purpose:** Create a standardized 8-section handoff document for the next AI session

**Command:**
```
/end handoff [project-number]
```

**Example:**
```
/end handoff 1
```

**What it does:**
1. Creates a new timestamped file: `projects/[project-name]/SESSION/YYYYMMDD-HHMMSS_handoff.md`
2. Uses the 8-section template from PATTERNS/HANDOFF_TEMPLATE_STANDARD.md:
   - Validation Checklist
   - Essential Files
   - Next Actions
   - Known Issues/Blockers
   - Project Context
   - Current Status
   - Key Decisions
   - Tips for Next Session
3. Updates WAITING_ON.md to reference the new handoff document

**Usage notes:**
- Use after completing significant work that another AI will continue
- Ensure validation questions test critical understanding
- Prioritize essential files in reading order
- Be specific with next actions

**Template location:**
`PATTERNS/HANDOFF_TEMPLATE_STANDARD.md`

---

**HANDOFF DEMO INTERACTION:**

User types: `2.1`

System:
```
Select project for handoff creation:
[1] example-project
[2] jarvis
[3] linkedin-campaign
[4] Create new project
[5] Return to SESSION END menu
```

User types: `1`

System:
```
Creating handoff document for example-project...
- Generating file: projects/example-project/SESSION/20251122-101500_handoff.md
- Using 8-section template
- Sections to complete:
  1. Validation Checklist
  2. Essential Files
  3. Next Actions
  4. Known Issues/Blockers
  5. Project Context
  6. Current Status  
  7. Key Decisions
  8. Tips for Next Session
- Updating WAITING_ON.md with reference to handoff

Would you like to:
[1] See template with fields to fill
[2] Return to SESSION END menu
[3] Return to MAIN menu
```

User types: `1`

System:
```
## HANDOFF TEMPLATE

# AI Handoff: memory-repo

## VALIDATION CHECKLIST
**IMPORTANT: Receiving AI must answer these before proceeding.**

1. What is the primary task you need to continue? [Enter task]
2. Which file should you read first? [Enter file]
3. What's the current blocker or challenge (if any)? [Enter blocker]

## ESSENTIAL FILES (READ IN THIS ORDER)
1. `[path/to/primary/file]` - [critical context]
2. `[path/to/secondary/file]` - [why needed]
3. [additional files in priority order]

[Additional sections...]

Type 'SUBMIT' when finished or 'CANCEL' to abort
```

---

## [1] SESSION START MENU

[1.1] Load project memory (quick)
[1.2] Load complete project context
[1.3] Start new project
[1.4] Return to main menu

## SLASH COMMANDS (SESSION START)

- `/start load` - Load project memory
- `/start full` - Load complete context
- `/start new` - Start new project
- `/menu` - Return to main menu

---

## [1.1] LOAD PROJECT MEMORY

**Purpose:** Quickly load essential context for a project

Select project to load:
[1] example-project
[2] jarvis
[3] linkedin-campaign
[4] Return to SESSION START menu

**What it does:**
1. Retrieves the WAITING_ON.md file for selected project
2. Displays current status, blockers, and next actions
3. Provides project-specific context
4. Ensures continuity from last session

---

## [3] PROJECT MANAGEMENT MENU

[3.1] List projects
[3.2] Create new project
[3.3] Check project status
[3.4] Return to main menu

## SLASH COMMANDS (PROJECT MANAGEMENT)

- `/project list` - List all projects
- `/project new` - Create new project
- `/project status` - Check project status
- `/menu` - Return to main menu

---

## [3.1] LIST PROJECTS

**Available Projects:**

[1] example-project
   - Status: Template complete (100%)
   - Last modified: 2025-11-21
   - Description: Template for project structure

[2] jarvis
   - Status: In development
   - Last modified: 2025-11-20
   - Description: Memory assistant project

[3] linkedin-campaign
   - Status: Planning phase
   - Last modified: 2025-11-19
   - Description: LinkedIn content campaign

[4] Return to PROJECT MANAGEMENT menu

---

## [7] MEMORY CHECK MENU

[7.1] Refresh memory - Reload memory patterns
[7.2] Check memory integrity
[7.3] Check PATTERNS/ folder usage
[7.4] Check project file maintenance
[7.5] Verify handoff compliance
[7.6] Return to main menu

## SLASH COMMANDS (MEMORY CHECK)

- `/memory refresh` - Reload memory patterns
- `/memory check` - Check memory integrity
- `/memory patterns` - Check PATTERNS/ folder usage
- `/memory maintenance` - Check file maintenance
- `/memory handoff` - Verify handoff compliance
- `/menu` - Return to main menu

---

## [7.1] REFRESH MEMORY

**Purpose:** Reload and utilize memory patterns defined in project files and PERSISTENT_MEMORY_LITE.md

**What it does:**
1. Reads key memory definition files:
   - PERSISTENT_MEMORY_LITE.md
   - PATTERNS/ directory files
   - Current project's PROJECT/ directory files
2. Refreshes the AI's understanding of memory patterns and structure
3. Re-establishes all memory constraints and enforcement patterns
4. Updates context with the latest memory organization rules

**Example output:**
```
Memory Refresh Complete:

✓ PERSISTENT_MEMORY_LITE.md loaded - Three-tier storage architecture active
✓ PATTERNS/VALIDATED_APPROACHES.md - 12 approaches loaded
✓ PATTERNS/ENFORCEMENT_PATTERNS.md - 8 patterns loaded
✓ PATTERNS/AI_FAILURE_MODES.md - 15 failure modes recognized
✓ PATTERNS/HANDOFF_TEMPLATE_STANDARD.md - 8-section format active
✓ PROJECT/COMMON_MISTAKES.md - 6 project-specific patterns loaded
✓ PROJECT/ARCHITECTURE_DECISIONS.md - 4 decisions recognized

Memory system refreshed and ready.
```

---

## [7.2] CHECK MEMORY INTEGRITY

**Purpose:** Perform a comprehensive check of the memory system integrity

**What it checks:**
1. All required files exist and are correctly structured
2. File maintenance is being performed properly (FIFO, line counts)
3. PATTERNS/ folder files are being referenced appropriately
4. Handoffs follow the standardized 8-section format
5. Timestamp-formatted chat folders are used correctly
6. Content is properly isolated between projects

**Example output:**
```
Memory System Check Results:

✓ Project structure: Valid
✓ PATTERNS/ folder: 3 files found, all referenced in the last 5 sessions
✓ File maintenance: All files under line limits
✓ Handoff compliance: Last handoff (20251121-193952) follows 8-section format
✓ Timestamp formats: All chat folders use YYYYMMDD-HHMMSS format
✓ Project isolation: No cross-project contamination detected

Recommendations:
- COMMON_MISTAKES.md approaching 450 lines, consider FIFO maintenance soon
- SESSION_LOG.md has 12 sessions, consider archiving oldest 2-3
```

---

## [7.2] CHECK PATTERNS/ FOLDER USAGE

**Purpose:** Verify that repository-wide patterns are properly utilized

**What it checks:**
1. Essential PATTERNS/ folder files exist
   - VALIDATED_APPROACHES.md
   - ENFORCEMENT_PATTERNS.md
   - AI_FAILURE_MODES.md
   - HANDOFF_TEMPLATE_STANDARD.md
2. These files are referenced in project files
3. PATTERNS/ folder content is being applied

**Example output:**
```
PATTERNS/ Folder Check Results:

✓ VALIDATED_APPROACHES.md: Referenced in 3 projects
✓ ENFORCEMENT_PATTERNS.md: Referenced in 2 projects
✓ AI_FAILURE_MODES.md: Referenced in last session
✓ HANDOFF_TEMPLATE_STANDARD.md: Used for all recent handoffs

Recommendations:
- Consider adding project-specific enforcement patterns for linkedin-campaign
- AI_FAILURE_MODES.md patterns may need review for the jarvis project
```

---

Type a number to navigate menus or use slash commands for direct access.
