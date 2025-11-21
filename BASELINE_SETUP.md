# Memory System Setup Guide

**Purpose:** First-time setup for new memory system users  
**Time Required:** 15-30 minutes  
**Prerequisites:** GitHub account, Claude Desktop (or other AI tool with GitHub access)

---

## Quick Start (5 Minutes)

**If you just want to try it:**

1. Clone this repository
2. **Simply type `menu` (not case-sensitive) at any time to access the interactive menu**
3. Or tell Claude: `Working on example-project. Read projects/example-project/PROJECT/WAITING_ON.md from memory-repo.`
4. If it works, you're done. If not, follow the full setup below.

---

## Full Setup Process

### Step 1: Clone Repository (2 min)

**Option A: HTTPS (Easier)**
```bash
git clone https://github.com/yourusername/memory-repo.git
cd memory-repo
```

**Option B: SSH (If you prefer SSH)**
```bash
git clone git@github.com:yourusername/memory-repo.git
cd memory-repo
```

**Verify:**
```bash
ls
# Should see: PATTERNS/, projects/, README.md, etc.
```

---

### Step 2: Configure GitHub Access (5-10 min)

**For Claude Desktop (Recommended):**

1. **Create GitHub Personal Access Token**
   - Go to: https://github.com/settings/tokens
   - Click "Generate new token (classic)"
   - Name: `claude-desktop-memory-repo`
   - Scopes: Check `repo` (full control)
   - Click "Generate token"
   - **Copy token immediately** (you won't see it again)

2. **Configure Claude Desktop**
   - Open: `$env:APPDATA\Claude\claude_desktop_config.json` (Windows)
   - Or: `~/Library/Application Support/Claude/claude_desktop_config.json` (Mac)
   - Add GitHub MCP server:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_token_here"
      }
    }
  }
}
```

3. **Restart Claude Desktop**
   - Quit completely (File → Quit)
   - Reopen

**For Other Tools:**
- ChatGPT: Use GitHub API with token
- VSCode/Cursor: Configure GitHub integration
- Custom tools: Implement GitHub API calls

---

### Step 3: Test Connection (2 min)

**In Claude Desktop, test:**

```
List files in memory-repo
```

**Expected result:** List of files/folders (PATTERNS/, projects/, README.md, etc.)

**If it fails:**
- Check token has `repo` scope
- Verify config file saved correctly
- Restart Claude Desktop again
- Check token not expired

---

### Step 4: Access the Menu System (1 min)

The simplest way to use the memory system is through the interactive menu:

1. Type `menu` (not case sensitive) at any time
2. You'll see the main menu with numbered options
3. Select options by typing the corresponding number
4. Navigate submenus the same way 
5. Use slash commands (e.g., `/project`) for direct access

**Example:**
```
menu
```

The AI will display the interactive menu with numbered options for all functions.

---

### Step 5: Create Your First Project (5 min)

**Option A: Use the Menu (Recommended)**

1. Type `menu` to load the menu system
2. Select "[3] PROJECT MANAGEMENT"
3. Select "[3.2] Create new project"
4. Follow the prompts to name your project

**Option B: Use Template Manually**

```bash
# Copy example project
cp -r projects/example-project projects/my-first-project

# Update placeholders manually or via script
# Replace [Project Name] → My First Project
# Replace [project-name] → my-first-project

git add projects/my-first-project
git commit -m "Create my-first-project from template"
git push
```

**Option C: Let AI Create It**

Tell Claude:
```
Create project my-first-project with structure:
- projects/my-first-project/PROJECT/ (warm storage)
- projects/my-first-project/SESSION/ (hot storage)
- Basic README.md

Use templates from projects/example-project/ as reference.
```

---

### Step 6: First Session (3 min)

**Load project via menu:**
```
menu
```
Then select "[1] SESSION START" and choose your project from the numbered list.

**Or load project directly:**
```
Working on my-first-project. Read projects/my-first-project/PROJECT/WAITING_ON.md from memory-repo.
```

**Initialize if empty:**
```
Update WAITING_ON.md with:
- RIGHT NOW: Setting up memory system
- NEXT ACTIONS: [your actual project tasks]
- PROJECT CONTEXT: [brief project description]
```

**Test write:**
```
Update projects/my-first-project/PROJECT/WAITING_ON.md:
Add to RECENT COMPLETIONS:
- [timestamp] Completed baseline setup and first memory test
```

**Verify:**
```bash
git pull
cat projects/my-first-project/PROJECT/WAITING_ON.md
# Should see your update
```

---

### Step 7: Creating a Handoff Document (5 min)

When ending a significant session or switching to another AI, create a handoff document:

**Via menu:**
1. Type `menu` to load the menu
2. Select "[2] SESSION END"
3. Select "[2.1] Create handoff"
4. Choose your project from the numbered list
5. Complete the 8-section template

**Direct command:**
```
Create a handoff document for my-first-project using the 8-section template:

1. Validation Checklist
2. Essential Files
3. Next Actions
4. Known Issues/Blockers
5. Project Context
6. Current Status
7. Key Decisions
8. Tips for Next Session
```

The handoff will be created as: `projects/my-first-project/SESSION/YYYYMMDD-HHMMSS_handoff.md`

---

## Three-Tier Storage Architecture

The memory system implements a **three-tier storage architecture**:

### 1. Cold Storage (PATTERNS/)
- Repository-wide knowledge and patterns
- Rarely changes
- 750-line limits per file

### 2. Warm Storage (PROJECT/)
- Project-specific information
- Changes frequently, but not every session
- 500-line FIFO maintenance per file

### 3. Hot Storage (SESSION/)
- Session-specific context
- Changes every session
- Includes timestamp-based chat folders (YYYYMMDD-HHMMSS_name)

---

## Verification Checklist

Before you start real work, verify:

- [ ] Can list files: `List files in memory-repo`
- [ ] Can read files: `Read MEMORY_MENU.md from memory-repo`
- [ ] Can write files: Successfully updated WAITING_ON.md
- [ ] Project created: Folder exists at projects/[your-project]
- [ ] Templates copied: All PROJECT files + SESSION files exist
- [ ] Git sync working: `git pull` shows your changes
- [ ] Menu system works: Type `menu` and see numbered options

---

## Common Setup Issues

### Issue: "Can't access repository"

**Cause:** MCP not configured or Claude Desktop not restarted

**Fix:**
1. Verify token in config: `$env:APPDATA\Claude\claude_desktop_config.json`
2. Restart Claude Desktop (quit completely, reopen)
3. Test: `List files in memory-repo`

---

### Issue: "GitHub tool unavailable"

**Cause:** MCP server not installed or wrong config

**Fix:**
1. Check `claude_desktop_config.json` has `mcpServers.github` section
2. Verify `npx` installed: `npx --version` (should show version)
3. If missing, install Node.js: https://nodejs.org/
4. Restart Claude Desktop

---

### Issue: "Permission denied" or "401 Unauthorized"

**Cause:** Token missing `repo` scope or expired

**Fix:**
1. Go to: https://github.com/settings/tokens
2. Find your token, regenerate if needed
3. Verify `repo` scope checked
4. Update token in config
5. Restart Claude Desktop

---

### Issue: "Files not syncing"

**Cause:** Git not pulling latest or conflicts

**Fix:**
```bash
git status  # Check state
git pull --rebase origin main  # Get latest
git push  # Push your changes
```

If conflicts:
```bash
# Resolve conflicts in editor
git add .
git rebase --continue
git push
```

---

## AI Memory Manager

The memory system works best when the AI adopts a "Memory Manager" persona that adapts to different contexts. This single role helps maintain consistency while providing specialized expertise for different memory tasks.

### Memory Manager: Core Responsibilities

**Essential Skills:**
- Strict file structure adherence
- Meticulous FIFO maintenance
- Strategic information organization
- Systematic session transitions
- Pattern recognition and implementation

**Operating Contexts:**
1. **Architect Context** - When designing system structure
2. **Librarian Context** - When organizing or retrieving knowledge
3. **Archivist Context** - When performing file maintenance
4. **Handoff Context** - When transferring work between sessions

### Using Memory Manager with Menu System

The menu system provides a framework for the Memory Manager to operate in the appropriate context:

- Use `/memory refresh` to initialize the Memory Manager role
- Menu options [1-3] primarily use Architect and Librarian contexts
- Menu option [5] primarily uses Archivist context
- Menu option [2.1] uses Handoff context

### Implementation Without VSCode Enforcement

Until VSCode enforcement tools are available:
1. At session start, tell the AI: "Operate as Memory Manager with [specific] context"
2. Use `menu` command to reinforce structure
3. Reference specific contexts when giving instructions: "As Archivist, perform FIFO maintenance..."

This single adaptive role approach provides specialized functionality without the overhead of managing multiple distinct roles.

## Next Steps

**After successful setup:**

1. Read PERSISTENT_MEMORY_LITE.md for system design
2. Type `menu` to explore all available commands
3. Tell the AI to "Operate as Memory Manager"
4. Start actual project work with memory enabled
5. Document mistakes in COMMON_MISTAKES.md as you discover them
6. Update WAITING_ON.md regularly

**Advanced:**
- Add ARCHITECTURE_DECISIONS.md if making design choices
- Set up FIFO archiving when files approach 500 lines
- Create multiple projects for different work streams
- Create timestamp-based chat folders for conversations (YYYYMMDD-HHMMSS_name)
- Use specific Memory Manager contexts for specialized tasks

---

## Support

**Documentation:**
- PERSISTENT_MEMORY_LITE.md - System design
- MEMORY_MENU.md - Interactive menu (type `menu` to access)
- projects/example-project/ - Template files

**Troubleshooting:**
- Check Claude Desktop logs if MCP issues
- Verify GitHub token hasn't expired
- Test with simple commands first before complex workflows

**Community:**
- GitHub Issues: Report bugs or request features
- Fork repo: Customize for your needs

---

**Setup Time:** 15-30 minutes first time, <5 minutes for additional projects  
**Maintenance:** Minimal (FIFO archiving when files exceed 500 lines)  
**Support:** Self-service via documentation + GitHub Issues

---

**Version:** 2.0 (Baseline)  
**Last Updated:** 2025-11-21  
**Status:** Production Ready
