# AI Memory System (Baseline)

**Conversational AI control framework with structured memory and continuity**

A methodology for managing complex, multi-session AI collaboration on projects. Provides structured memory, session continuity, and project governance for AI conversations.

---

## What This Does

Without structure, AI conversations are chaotic. You repeat yourself. AI forgets decisions. Work gets duplicated. Mistakes happen twice. Each session starts from zero.

This system provides **conversational control** through structured memory files that enforce continuity across sessions. The AI operates within your defined project structure, maintains state, and builds on previous work instead of restarting.

**What it controls:**
- **Session continuity** - AI remembers previous conversations
- **Context management** - AI knows what's relevant
- **Decision tracking** - Prevents contradicting past decisions
- **Error prevention** - AI learns from documented mistakes
- **Project isolation** - Keeps projects independent and self-contained

**It's not just memory—it's methodology:**
- How to start sessions (load state)
- How to track progress (structured updates)
- How to prevent errors (documented patterns)
- How to maintain continuity (persistent context)

**Memory Manager Persona:**
The system works best with a single "Memory Manager" persona that adapts to different contexts (Architect, Librarian, Archivist, Handoff). See BASELINE_SETUP.md for details on implementing this persona.

**AI-agnostic:** Works with any AI that can read/write to GitHub (Claude with MCP, Cursor, VS Code with extensions, manual Git workflow)

---

## Three-Tier Storage Architecture

This memory system implements a **three-tier storage architecture** for optimal knowledge management:

### 1. Cold Storage (PATTERNS/)
- Repository-wide knowledge and patterns
- Rarely changes
- 750-line limits per file
- Contains validated approaches, enforcement patterns, and failure modes

### 2. Warm Storage (PROJECT/)
- Project-specific information
- Changes frequently but not every session
- 500-line FIFO maintenance per file
- Includes project status, lessons learned, architecture decisions

### 3. Hot Storage (SESSION/)
- Session-specific context
- Changes every session
- 100/500-line FIFO maintenance
- Contains current context, session logs, and timestamp-based chat folders

This tiered approach ensures information is stored at the appropriate level of persistence and accessibility.

---

## Project Isolation Principle

**IMPORTANT: All documents MUST be created within their project folder**

When working in a specific project (e.g., "example-project"), all new files and documents must be created within that project's directory structure:

```
projects/example-project/PROJECT/  - For project management files
projects/example-project/SESSION/  - For session-specific files
projects/example-project/DOCUMENTS/ - For project-specific content
```

**NEVER create project files in the repository root!**

Creating files outside the active project violates isolation and persistence requirements. Each project must maintain complete independence. AIs must strictly enforce this boundary to prevent cross-project contamination.

---

## File Structure

```
your-repo/
├── README.md (this file - start here)
├── BASELINE_SETUP.md (setup instructions)
├── PERSISTENT_MEMORY_LITE.md (system design)
├── MEMORY_MENU.md (interactive menu system - type "menu" to access)
├── PATTERNS/ (cold storage - repository-wide knowledge)
│   ├── VALIDATED_APPROACHES.md (proven methodology patterns)
│   ├── ENFORCEMENT_PATTERNS.md (constraint patterns for AIs)
│   └── AI_FAILURE_MODES.md (common AI mistakes and solutions)
└── projects/ (project-specific directories)
    └── example-project/ (template for new projects)
        ├── README.md (project overview)
        ├── PROJECT/ (warm storage - project management)
        │   ├── WAITING_ON.md (current status) ← Start here
        │   ├── COMMON_MISTAKES.md (lessons learned)
        │   └── ARCHITECTURE_DECISIONS.md (key decisions)
        ├── SESSION/ (hot storage - session management)
        │   ├── CURRENT_CONTEXT.md (session state)
        │   ├── SESSION_LOG.md (session history)
        │   └── YYYYMMDD-HHMMSS_name/ (timestamp chat folders)
        │       └── chat.log (conversation record)
        └── DOCUMENTS/ (project-specific content)
            └── SAMPLE_DOCUMENT.md (project documentation)
```

---

## Quick Start

**IMPORTANT: At any time, simply type `menu` (not case sensitive) to load the interactive menu system.**

### 1. Use This Template

Click green "Use this template" button above → Create your own repository

### 2. Choose Your Access Method

**Option A: AI with GitHub Integration**
- **Claude Desktop:** See [Claude Desktop Setup](#claude-desktop-setup) below
- **Cursor / VS Code:** Built-in GitHub support through extensions
- **Other AI platforms:** Check if they support GitHub API integration

**Option B: Manual Git Workflow**
- Clone repository locally
- Edit files in any text editor
- Copy/paste content to AI when starting sessions
- Update files based on AI's work
- Commit and push changes via command line or Git GUI

### 3. Start Your First Session

**With GitHub Integration (Claude Desktop, Cursor, etc.):**

```
Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md from [your-repo-name].
```

AI loads current status and continues from last session.

**Without GitHub Integration (Manual workflow):**

1. Open `projects/example-project/PROJECT/WAITING_ON.md` locally
2. Copy contents
3. Paste into AI chat with:
```
Working on example-project.

Current status:
[paste WAITING_ON.md contents]

Continue from where we left off.
```

---

## User Guide

### Universal Menu Access

**Type `menu` anytime (not case sensitive) to access the interactive menu system.**

This is a persistent rule throughout the entire memory system. No matter what context or state you're in, typing "menu" (or "MENU" or "Menu") will always load the interactive menu from MEMORY_MENU.md, allowing you to:
- Navigate all system features through numbered options
- Access projects through numbered selection
- Use slash commands for direct access to specific functions

### Starting a Session

**With GitHub Integration (Claude Desktop, Cursor, etc.):**

```
Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md from [your-repo-name].
```

AI loads current status and continues from last session.

**Without GitHub Integration (Manual workflow):**

1. Open `projects/example-project/PROJECT/WAITING_ON.md` locally
2. Copy contents
3. Paste into AI chat with:
```
Working on example-project.

Current status:
[paste WAITING_ON.md contents]

Continue from where we left off.
```

### During a Session

**Quick menu access:**
```
menu
```
Loads the interactive menu system with numbered navigation options.

**Update status:**
```
Update WAITING_ON.md:
- Add to RECENT COMPLETIONS: [what was done]
- Update blockers if any
- Update next actions
```

**Document a lesson:**
```
Add to COMMON_MISTAKES.md:
Pattern X: [what went wrong]
- Issue: [description]
- Fix: [solution]
```

**Log a decision:**
```
Add to ARCHITECTURE_DECISIONS.md:
Decision X: [what was decided]
- Context: [why this came up]
- Decision: [what we chose]
- Rationale: [why]
```

### Ending a Session

**With GitHub Integration:**

AI proposes updates to WAITING_ON.md. Review and approve. AI commits directly to GitHub.

**Manual workflow:**

1. Review AI's proposed changes to WAITING_ON.md
2. Copy updated content to local file
3. Commit and push:
```bash
git add projects/example-project/PROJECT/WAITING_ON.md
git commit -m "Session complete: [brief summary]"
git push
```

### AI Session Handoffs

**Creating a handoff document:**

When ending a significant session or transferring work to another AI, create a formal handoff:

```
Create a handoff document:
- Save as: SESSION/YYYYMMDD-HHMMSS_handoff.md
- Include current status, essential files list, and next steps
- Update WAITING_ON.md to reference the handoff
```

**Benefits of structured handoffs:**
- Eliminates repetition between sessions
- Ensures critical decisions are preserved
- Provides clear reading order for files
- Improves continuity with detailed context

For full protocol and template, see [PATTERNS/AI_HANDOFF_PROTOCOL.md](PATTERNS/AI_HANDOFF_PROTOCOL.md).

### Next Session

AI loads WAITING_ON.md again and sees:
- What was completed last session
- Current blockers
- Next actions
- Recent completions

Continuity maintained across sessions without re-explaining context.

### Creating New Projects

```bash
# Copy example project
cp -r projects/example-project projects/new-project-name

# Edit files to match your project
# Then commit
git add projects/new-project-name
git commit -m "Add new-project-name"
git push
```

Tell AI:
```
Working on new-project-name. Read projects/new-project-name/PROJECT/WAITING_ON.md from [repo-name].
```

---

## PATTERNS Directory

The PATTERNS directory contains repository-wide knowledge that applies across all projects. This is the "cold storage" tier in the three-tier architecture.

### VALIDATED_APPROACHES.md
Documents proven AI collaboration methodologies that have been validated to improve outcomes. Each approach includes:
- What the approach is
- Why it works
- Implementation details
- When to use it

### ENFORCEMENT_PATTERNS.md
Contains structural constraint patterns that improve AI reliability. These patterns establish guardrails for AI behavior, focusing on:
- Constraint-based guidance over role prompting
- Checkpoint gates for quality control
- Evidence requirements for verification
- Implementation patterns for consistency

### AI_FAILURE_MODES.md
Documents common ways AIs fail and how to prevent these failures. Each failure mode includes:
- Pattern description
- Root cause analysis
- Solution implementation
- Examples of before/after

These patterns are designed to be used by any AI interacting with the repository, providing universal guidance while protecting against common failure modes.

---

## File Maintenance

### FIFO Maintenance

Files with size limits require First-In-First-Out (FIFO) maintenance:

**PROJECT/ files (500-line limit):**
- WAITING_ON.md - Archive oldest entries when approaching 500 lines
- COMMON_MISTAKES.md - Archive oldest P3 patterns when approaching 500 lines
- ARCHITECTURE_DECISIONS.md - No strict line limit, but organize by importance

**SESSION/ files:**
- CURRENT_CONTEXT.md - 100-line target, compress when exceeding
- SESSION_LOG.md - 500-line FIFO, archive oldest sessions
- chat.log - 750-line target per conversation

When files approach their limits:
1. Create ARCHIVE/ directory if needed
2. Move oldest content to dated archive file
3. Keep most recent/relevant information in main file

---

## Complete Example: First Session

**You:**
```
Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md from [your-repo-name].
```

Or simply:
```
menu
```
To load the interactive menu system and select a project from numbered options.

**AI:**
```
[Reads WAITING_ON.md]

Current status:
- Active: Example project setup
- No blockers
- Next actions: Begin project work
- Recent completions: Project structure created

Ready to continue. What should we work on?
```

**You:**
```
Let's add a new task to track. Add to WAITING_ON.md that we need to create documentation for a new feature.
```

**AI:**
```
[Proposes update to WAITING_ON.md]

Updated WAITING_ON.md with:
- Added to NEXT ACTIONS: Create documentation for new feature
- Updated timestamp

Changes committed to GitHub. Anything else?
```

**Next session tomorrow:**
```
Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md from [your-repo-name].
```

**AI:**
```
[Reads WAITING_ON.md]

Current status shows we need to create documentation for new feature.
I remember we discussed this yesterday. Ready to start?
```

**That's continuity.** AI remembers without you re-explaining.

---

## Control Framework Benefits

### 1. Decision Consistency
AI references `ARCHITECTURE_DECISIONS.md` before suggesting changes. No contradictions.

### 2. Error Prevention
AI checks `COMMON_MISTAKES.md` before proposing solutions. Learned patterns are applied.

### 3. Session Continuity
AI reads `WAITING_ON.md` to understand current state. No context loss between sessions.

### 4. Project Governance
Structured files enforce methodology. AI operates within defined boundaries.

### 5. Version Control
GitHub tracks all changes. See history of decisions, rollback if needed.

### 6. Project Isolation
Each project is fully self-contained. No cross-project contamination.

---

## Claude Desktop Setup

If you're using Claude Desktop with MCP (Model Context Protocol), follow these additional steps:

### 1. Create GitHub Token

1. Go to: https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Give it a name (e.g., "Claude MCP Access")
4. Select scope: `repo` (full control of private repositories)
5. Click "Generate token"
6. **Copy token immediately** (you won't see it again)

### 2. Configure Claude Desktop

**Windows:**
```
%APPDATA%\Claude\claude_desktop_config.json
```

**Mac:**
```
~/Library/Application Support/Claude/claude_desktop_config.json
```

**Linux:**
```
~/.config/Claude/claude_desktop_config.json
```

Edit the file and add:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_token_here"
      }
    }
  }
}
```

Replace `your_token_here` with your actual token.

### 3. Restart Claude Desktop

Fully quit and restart Claude Desktop for changes to take effect.

### 4. Test Connection

In Claude:
```
List files in [your-repo-name]
```

Should see: README.md, BASELINE_SETUP.md, projects/, etc.

### 5. Start Using

```
Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md from [your-repo-name].
```

Success! Claude now has persistent memory through GitHub.

---

## Support

- **Issues:** Use GitHub Issues on this repository
- **Questions:** Review README.md for detailed examples
- **Setup help:** See [BASELINE_SETUP.md](BASELINE_SETUP.md) for troubleshooting

---

**What it is:** Conversational AI control framework with structured memory  
**What it does:** Maintains continuity across AI sessions through project governance  
**Time to first use:** 15-30 minutes  
**Prerequisites:** GitHub account  
**Optional:** AI platform with GitHub integration (Claude Desktop + MCP, Cursor, VS Code, etc.)  
**Works without integration:** Yes - manual Git workflow fully supported
