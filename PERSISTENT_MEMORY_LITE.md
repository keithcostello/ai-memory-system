# Persistent Memory System - Lite Version

**Purpose:** Standalone memory system without Framework V2.9.2 dependency  
**Version:** 1.0 (Baseline)  
**Date:** 2025-11-21  
**Status:** Production Ready

---

## Overview

This is a **GitHub-backed memory system** that provides AI sessions with persistent context across conversations, projects, and tool boundaries (Claude.ai, ChatGPT, VSCode extensions, etc.).

**Core Principle:** Memory is stored in GitHub. AIs read/write via GitHub MCP integration (Claude Desktop) or API calls (other tools).

---

## Architecture

### Three-Tier Storage

**Cold Storage (PATTERNS/):**
- Rarely changes
- 750-line limits per file
- Repository-wide patterns, approaches, and templates

**Warm Storage (PROJECT/):**
- Changes frequently
- 500-line FIFO per file
- Current status, lessons learned, architecture

**Hot Storage (SESSION/):**
- Changes every session
- 500-line FIFO for logs, <100 target for context
- Session-specific work details

---

## File Structure

```
your-repository/
├── PATTERNS/               # Cold storage - repository-wide knowledge
│   ├── VALIDATED_APPROACHES.md
│   ├── ENFORCEMENT_PATTERNS.md
│   ├── AI_FAILURE_MODES.md
│   └── HANDOFF_TEMPLATE_STANDARD.md
├── projects/
│   └── [project-name]/
│       ├── PROJECT/        # Warm storage (500-line FIFO)
│       │   ├── WAITING_ON.md
│       │   ├── COMMON_MISTAKES.md
│       │   └── ARCHITECTURE_DECISIONS.md  (optional)
│       ├── SESSION/        # Hot storage
│       │   ├── CURRENT_CONTEXT.md  (<100 lines target)
│       │   ├── SESSION_LOG.md      (500-line FIFO)
│       │   ├── YYYYMMDD-HHMMSS_name/  (timestamp chat folders)
│       │   │   └── chat.log        (750-line target)
│       │   └── YYYYMMDD-HHMMSS_handoff.md  (session handoffs)
│       ├── DOCUMENTS/      # Project-specific content
│       │   └── [project files]
│       └── README.md
├── MEMORY_MENU.md          # Quick command reference
└── README.md               # Project overview
```

---

## Core Files

### WAITING_ON.md (PROJECT/)

**Purpose:** Current work state for this project

**Sections:**
1. RIGHT NOW - Current active work
2. ACTIVE BLOCKERS - What's blocking progress
3. WAITING FOR [HUMAN] - Decisions/approvals needed
4. NEXT ACTIONS QUEUE - Immediate/queued/future tasks
5. RECENT COMPLETIONS - Last 10 items done
6. PROJECT CONTEXT - High-level status

**Maintenance:** 500-line FIFO, archive to ARCHIVE/ when exceeded

---

### COMMON_MISTAKES.md (PROJECT/)

**Purpose:** Document lessons learned during this project

**Format:**
```markdown
## MEMORY INDEX
**P1 (Critical):** [Always check these]
**P2 (Important):** [Check often]
**P3 (Reference):** [Check when relevant]

## PATTERN N: [Title]
**Documented:** Session X - Date
**Severity:** P1/P2/P3
**Category:** [Architecture/Process/Technical/Documentation]

**What Went Wrong:**
- ❌ [Mistake]

**Correct Approach:**
- ✅ [Fix]

**Why This Matters:**
[Explanation]
```

**Maintenance:** 500-line FIFO, archive P3 patterns when exceeded, keep P1/P2

---

### ARCHITECTURE_DECISIONS.md (PROJECT/ - Optional)

**Purpose:** Document major technical decisions and rationale

**Format:**
```markdown
## DECISION: [Title]
**Date:** YYYY-MM-DD
**Decider:** [Who]
**Status:** Accepted/Superseded/Deprecated

**Context:** [Problem/situation]
**Decision:** [What was chosen]
**Alternatives Considered:** [Options A, B, C with pros/cons]
**Rationale:** [Why this choice]
**Consequences:** [Benefits, tradeoffs, technical debt]
```

**Maintenance:** No line limit (architecture decisions don't expire)

---

### CURRENT_CONTEXT.md (SESSION/)

**Purpose:** Quick summary for fast context loading

**Target:** <100 lines

**Sections:**
1. TL;DR - 3 sentences: what we did, what's next, open questions
2. Last Session Summary - Outcome, completions, decisions, issues
3. Active Context - Branch, files, dependencies
4. Next Session Should - Priority actions, pre-work checks

**Maintenance:** Compress when exceeding 100 lines

---

### SESSION_LOG.md (SESSION/)

**Purpose:** Detailed narrative of work sessions

**Format:**
```markdown
## Session N - Date
**Session ID:** [id]
**AI:** [name/tool]
**Duration:** [hours]

### Objective
[Goal]

### Context
[Starting state]

### Work Performed
[Phases with actions/results/files]

### Decisions Made
[Numbered list with context/choice/rationale/impact]

### Issues Discovered
[Problem/impact/status/resolution]

### Outcomes
[Completed/incomplete/blockers]

### Next Session
[Should start with / Should avoid / Context needed]
```

**Maintenance:** 500-line FIFO, keep 10-15 recent sessions, archive older

---

## AI Handoff Protocol

### YYYYMMDD-HHMMSS_handoff.md (SESSION/)

**Purpose:** Transfer context between AI sessions

**Format:**
```markdown
# AI Handoff: [Project Name]

## Session Information
**Date:** [YYYY-MM-DD]
**Time:** [HH:MM]
**AI:** [Your identifier]
**Session Duration:** [Approximate time]
**Repository:** [Repository name]

## Project Context
Brief overview of the project (2-3 sentences)

## Current Status
* **Phase:** [Design/Implementation/Testing/etc.]
* **Progress:** [%] complete
* **Last Activity:** [Brief description of last completed task]
* **Environment:** [Relevant configuration, versions, etc.]

## Essential Files (Read In This Order)
1. `projects/[project]/PROJECT/WAITING_ON.md` - Current project state
2. `projects/[project]/PROJECT/COMMON_MISTAKES.md` - Project-specific pitfalls
3. `projects/[project]/SESSION/CURRENT_CONTEXT.md` - Recent session context
4. [Additional critical files in recommended reading order]

## Key Decisions
* **Decision 1:** [Brief explanation] (See `projects/[project]/PROJECT/ARCHITECTURE_DECISIONS.md#decision-x`)
* **Decision 2:** [Brief explanation with file reference]
* **[Additional decisions...]**

## Open Issues
* **Issue 1:** [Description and current state]
* **Issue 2:** [Description and current state]
* **[Additional issues...]**

## Next Steps
1. [First task with any specific instructions]
2. [Second task...]
3. [Additional tasks in priority order]

## Tips for Next Session
* [Important reminder or guidance]
* [Suggestion on approach]
* [Areas to be careful with]

## Unresolved Questions
* [Question that needs answering]
* [Decision that needs making]
* [Information that needs gathering]
```

**Maintenance:** Create new handoff file for each significant session transition

---

## PATTERNS/ Directory Usage

The PATTERNS/ directory contains repository-wide knowledge that applies across all projects. This is the "cold storage" tier in the three-tier architecture. Unlike project-specific files, these patterns should be referenced by all projects.

### Key PATTERNS Files

**VALIDATED_APPROACHES.md:**
- **Purpose:** Documents proven methodologies and techniques that have been validated to improve outcomes
- **Usage:** Reference when starting new tasks or when facing challenging problems
- **Format:** Each approach includes:
  - What the approach is
  - Why it works
  - Implementation details
  - When to use it
- **Reference pattern:** "Following the validated approach from PATTERNS/VALIDATED_APPROACHES.md#[approach-name]..."

**ENFORCEMENT_PATTERNS.md:**
- **Purpose:** Contains structural constraint patterns that improve AI reliability
- **Usage:** Apply as guardrails for AI behavior, especially for critical tasks
- **Format:** Each pattern includes:
  - Constraint description
  - Implementation guidance
  - Verification methods
  - Example implementation
- **Reference pattern:** "Implementing enforcement pattern from PATTERNS/ENFORCEMENT_PATTERNS.md#[pattern-name]..."

**AI_FAILURE_MODES.md:**
- **Purpose:** Documents common ways AIs fail and how to prevent these failures
- **Usage:** Review before implementing complex solutions to avoid known pitfalls
- **Format:** Each failure mode includes:
  - Pattern description
  - Root cause analysis
  - Prevention measures
  - Examples of before/after
- **Reference pattern:** "Avoiding the failure mode documented in PATTERNS/AI_FAILURE_MODES.md#[failure-name]..."

**HANDOFF_TEMPLATE_STANDARD.md:**
- **Purpose:** Standardized 8-section template for AI handoffs
- **Usage:** Use when creating handoff documents between AI sessions
- **Format:** Contains the complete 8-section structure:
  - Validation Checklist
  - Essential Files
  - Next Actions
  - Known Issues/Blockers
  - Project Context
  - Current Status
  - Key Decisions
  - Tips for Next Session
- **Reference pattern:** "Creating handoff using PATTERNS/HANDOFF_TEMPLATE_STANDARD.md template..."

### When to Reference PATTERNS/

**During Project Planning:**
- Review VALIDATED_APPROACHES.md for best practices
- Apply relevant ENFORCEMENT_PATTERNS.md constraints
- Check AI_FAILURE_MODES.md for potential pitfalls

**During Implementation:**
- Reference specific approaches from VALIDATED_APPROACHES.md
- Apply enforcement patterns for critical sections
- Document new failure modes as discovered

**During Handoffs:**
- Use HANDOFF_TEMPLATE_STANDARD.md for all handoff documents
- Reference relevant patterns being applied in the project

**When Documenting Mistakes:**
- Check if the mistake is already in AI_FAILURE_MODES.md
- If not, consider adding it to both project COMMON_MISTAKES.md and AI_FAILURE_MODES.md

### How to Update PATTERNS/

1. **Adding New Content:**
   - Use the established format for each file type
   - Ensure new content is repository-wide (not project-specific)
   - Add clear examples and implementation guidance

2. **Maintenance:**
   - 750-line limit per file
   - Archive older, less critical patterns when approaching limit
   - Maintain categorization and indexing for easy reference

3. **Cross-References:**
   - When adding to project files, reference relevant PATTERNS
   - When adding to PATTERNS, update relevant project files if needed

---

## Usage Patterns

### Session Start

**Minimal context load:**
```
Working on [project-name]. Read projects/[project-name]/PROJECT/WAITING_ON.md from your-repository.
```

**Full context load:**
```
Load complete context:
1. projects/[project-name]/PROJECT/WAITING_ON.md
2. projects/[project-name]/PROJECT/COMMON_MISTAKES.md
3. projects/[project-name]/SESSION/CURRENT_CONTEXT.md
```

**Using handoff for context:**
```
Working on [project-name]. Read the handoff document referenced in WAITING_ON.md, then follow the Essential Files reading order.
```

---

### Session End

**Update memory:**
```
Update session context:
1. SESSION/CURRENT_CONTEXT.md - What we did, what's next
2. SESSION/SESSION_LOG.md - Add Session [N] entry
3. PROJECT/WAITING_ON.md - Update status if changed
```

**Create handoff for next session:**
```
Create AI handoff document:
1. Create SESSION/YYYYMMDD-HHMMSS_handoff.md with proper template
2. Include Essential Files reading order
3. List all key recent decisions
4. Set clear next steps
5. Update WAITING_ON.md to reference the handoff
```

---

### Document Mistake

```
Add to projects/[project-name]/PROJECT/COMMON_MISTAKES.md:

### Pattern [N]: [Title]
- ❌ [What not to do]
- ✅ [What to do instead]
- **Why:** [Explanation]
- **Documented:** [Session reference]
```

---

### Record Decision

```
Add to projects/[project-name]/PROJECT/ARCHITECTURE_DECISIONS.md:

## DECISION: [Name]
**Date:** [YYYY-MM-DD]
**Context:** [Why decision needed]
**Decision:** [What we chose]
**Rationale:** [Why this choice]
**Consequences:** [Trade-offs]
```

---

## File Maintenance (FIFO)

### Trigger Conditions

**500-line files:**
- WAITING_ON.md
- COMMON_MISTAKES.md
- SESSION_LOG.md

**When file approaches 500 lines (450+ recommended):**

1. Create ARCHIVE/ directory if needed
2. Copy old content to `ARCHIVE/[filename]_YYYY-MM-DD.md`
3. Remove old content from main file
4. Keep recent/critical content

**Exception:** COMMON_MISTAKES.md keeps all P1/P2 patterns, archives only P3

---

### Archive Strategy

**WAITING_ON.md:**
- Archive RECENT COMPLETIONS section
- Keep RIGHT NOW, BLOCKERS, WAITING FOR, QUEUE

**COMMON_MISTAKES.md:**
- Archive P3 patterns
- Keep P1/P2 patterns
- Update Memory Index

**SESSION_LOG.md:**
- Archive sessions older than 10-15 most recent
- Keep recent sessions

---

## Tool Integration

### Claude Desktop (MCP)

**Setup:** Configure GitHub MCP server in `claude_desktop_config.json`

**Commands:**
- `Read [file] from your-repository`
- `Write to [file] in your-repository`
- `List [directory] from your-repository`

---

### ChatGPT / Other AIs

**Requirements:**
- GitHub API access
- Personal access token with repo scope

**Integration:** Use GitHub API calls or custom MCP implementation

---

### VSCode Extensions

**Kilo Code MCP Extension:**
- Auto-detected if configured
- Same commands as Claude Desktop

**Manual Integration:**
- Read files via GitHub API
- Write files via commits
- Requires token setup

---

## Project Setup

### New Project Creation

**Option 1: Use Template (Recommended)**

```bash
# Copy projects/example-project/ to new project
cp -r projects/example-project projects/[new-project-name]

# Update placeholders in all files
# - Replace [Project Name]
# - Replace [project-name]
# - Update dates, session IDs, etc.

git add projects/[new-project-name]
git commit -m "Create [new-project-name] from template"
git push
```

**Option 2: Manual Creation**

```bash
mkdir -p projects/[project-name]/{PROJECT,SESSION}

# Copy templates from example-project
# Or create files manually following structure
```

---

### First Session

1. Load memory: `Working on [project-name]`
2. Verify files exist: WAITING_ON.md, COMMON_MISTAKES.md
3. Initialize WAITING_ON.md with current task
4. Begin work
5. Update memory at session end

---

## Multi-Project Usage

**Project isolation:** Each project has own PROJECT/ and SESSION/ folders

**Cross-project patterns:** Store in PATTERNS/ directory (cold storage)

**User-level tracking:** Not included in Lite version (by design)

---

## Design Principles

### Principle 1: GitHub as Single Source of Truth

Memory persists in GitHub repository. All tools read/write via GitHub integration.

**Why:** No manual file transfers, automatic sync, version control, multi-tool access

---

### Principle 2: FIFO Maintenance

500-line limit prevents memory files from becoming unmanageable. Old content archives automatically.

**Why:** Keep context window bounded, maintain relevance, preserve history

---

### Principle 3: Project-Scoped Memory

Each project tracks its own status, mistakes, and decisions independently.

**Why:** Project isolation, no cross-project contamination, clear boundaries

---

### Principle 4: Tool Agnostic

Works with any AI tool that can access GitHub (Claude.ai, ChatGPT, Cursor, VSCode, etc.)

**Why:** Not locked to single vendor, user controls memory, extensible

---

### Principle 5: Minimal Mandatory Structure

Only WAITING_ON.md and COMMON_MISTAKES.md required. Everything else optional.

**Why:** Start simple, add complexity only when needed, low barrier to entry

---

## Memory System Integrity

### Refreshing Memory Patterns

The memory system includes functionality to refresh the AI's understanding of memory patterns and rules. This is useful when starting a new session or when switching between projects.

**To refresh memory patterns:**
1. Type `menu` to access the interactive menu
2. Select "[7] MEMORY CHECK"
3. Select "[7.1] Refresh memory"

**Or use slash command:**
- `/memory refresh` - Reload memory patterns from PERSISTENT_MEMORY_LITE.md and project files

**What gets refreshed:**
- Three-tier storage architecture (cold/warm/hot)
- PATTERNS folder usage guidelines
- Project-specific patterns and constraints
- Enforcement patterns for memory consistency
- File maintenance rules and FIFO protocols
- Handoff template format and requirements

**When to refresh memory:**
- At the start of a new AI session
- When switching between projects
- After updating PATTERNS/ folder files
- If memory inconsistencies are detected

### Running Memory Checks

The memory system includes built-in verification mechanisms to ensure proper usage and maintenance. These checks can be accessed through the Memory Check menu.

**To run a memory check:**
1. Type `menu` to access the interactive menu
2. Select "[7] MEMORY CHECK"
3. Choose the type of check to run

**Or use slash commands:**
- `/memory refresh` - Reload memory patterns
- `/memory check` - Check memory integrity
- `/memory patterns` - Check PATTERNS/ folder usage
- `/memory maintenance` - Check file maintenance
- `/memory handoff` - Verify handoff compliance

**What gets checked:**
- File existence and structure
- Line count maintenance (FIFO compliance)
- PATTERNS/ folder usage and references
- Handoff format compliance
- Timestamp format correctness
- Project isolation integrity

**Using memory check results:**
- Address any issues identified
- Perform recommended maintenance actions
- Update documentation based on findings
- Improve process adherence

---

## Differences from Full Framework Version

**Removed:**
- External framework dependencies
- Sprint planning workflows
- Complex AI-to-AI communication protocols
- UAT gates and testing infrastructure
- PM/Developer role separation

**Added:**
- Interactive menu system with numbered navigation
- Simple "menu" command access from anywhere
- Memory check system with slash commands
- 8-Section handoff protocol for session continuity
- Timestamp-formatted chat folders
- Project structure competency requirements
- Session-to-session continuity mechanisms
- Clear file reading order priorities

**Kept:**
- GitHub-backed storage
- Three-tier memory (cold/warm/hot)
- FIFO maintenance (500-line limits)
- Project isolation
- Pattern documentation
- Decision recording

**Result:** Standalone memory system with improved usability and navigation

---

## Getting Started

**Step 1:** Clone this repository  
**Step 2:** Configure GitHub MCP (Claude Desktop) or API access (other tools)
**Step 3:** Test connection: `List files in your-repository`
**Step 4:** Create project from template: Copy `projects/example-project/`
**Step 5:** Start session: `Working on [project-name]`  
**Step 6:** Reference MEMORY_MENU.md for commands

---

## Troubleshooting

**Can't access repository:**
- Restart Claude Desktop (if using MCP)
- Verify GitHub token has repo access
- Check config: `$env:APPDATA\Claude\claude_desktop_config.json`

**Files not syncing:**
- Pull latest: `git pull --rebase origin main`
- Check for conflicts: `git status`
- Resolve manually if needed

**Lost context:**
- Read SESSION_LOG.md last entry
- Read CURRENT_CONTEXT.md
- Read WAITING_ON.md for current state

---

## Version History

**1.0 (2025-11-21):** Initial Lite version (Framework IP extracted, standalone)

---

**Lines:** ~450  
**Target Audience:** Users without Framework V2.9.2 knowledge  
**Dependencies:** GitHub access only  
**Status:** Production Ready
