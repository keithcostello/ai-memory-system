START HERE: AI Memory System Quick Guide
Welcome to the AI Memory System! This guide helps both humans and AIs get started in 5 minutes.

What Is This? (30 Seconds)
This system gives AIs persistent memory across conversations using structured files stored in GitHub. It solves the problem of AIs forgetting context between sessions.
Key benefit: Work on complex projects across multiple sessions without repeating yourself.

First Steps
For AI Reading This:
Your immediate actions:

Tell the user: "Type menu to see all available options"
Explain the menu system:

The menu provides numbered options for all system functions
Options include: SESSION START, PROJECT MANAGEMENT, MEMORY CHECK, and more
Users can type numbers (like 1) or slash commands (like /project list)


When the user types menu, guide them through selecting option [1.1] to load the example-project
After loading the project, explain what you found in WAITING_ON.md
Suggest 2-3 practical ways they could use this system for their work

Your role: Act as Memory Manager - guide the user through learning the system by doing.
For Humans:

Clone this repository to your local machine
Tell your AI: "Read the START_HERE.md file"
The AI will guide you through the rest


AI Quick Reference
Core Commands:

menu - Show all system options (use this first)
Type numbers to select menu options (e.g., 1 for SESSION START)
Use slash commands for direct access (e.g., /project list)

Your workflow:

At session start, guide user to type menu
Help them select [1.1] Load project memory
Read the WAITING_ON.md file for that project
Explain current status and suggest next actions
Update files as work progresses
At session end, create a handoff document


Example: Your First Session
Human: I just cloned the repo. What now?
AI: Great! Type menu to see all available options. This will show you the main menu with numbered choices for managing your projects and memory.
Human: menu
AI:
🚀 MAIN MENU

[1] SESSION START - Load project memory
[2] SESSION END - Update memory and handoff  
[3] PROJECT MANAGEMENT - Create/list/manage projects
[4] DOCUMENTATION - Record mistakes/decisions
[5] FILE OPERATIONS - Read/write/list files
[6] STATUS CHECKS - View project status
[7] MEMORY CHECK - Verify memory system integrity
[8] TROUBLESHOOTING - Resolve common issues
[9] HELP - Get assistance

Type a number or use slash commands like /project list
Let's start by loading the example project. Type 1 to go to SESSION START.
Human: 1
AI:
SESSION START MENU

[1.1] Load project memory (quick)
[1.2] Load complete project context
[1.3] Start new project
[1.4] Return to main menu
Type 1.1 to load the example-project and see how the system works.
Human: 1.1
AI:
Available projects:
[1] example-project

Select a project number:
Human: 1
AI: [Reading projects/example-project/PROJECT/WAITING_ON.md]
Here's what's in the example project:
Current Status:

Active: Example project template setup
Blockers: None
Next Actions: Begin using the template for real work

How you could use this system:

For Software Projects: Track bugs, feature decisions, and architecture choices across multiple AI coding sessions
For Writing Projects: Maintain story continuity, character details, and plot decisions across writing sessions
For Research: Document findings, track sources, and build knowledge progressively

Want to try creating your own project? Type menu then select [3.2] to create a new project.

System Structure (30 Seconds)
your-repo/
├── PATTERNS/             # Repository-wide knowledge (rarely changes)
├── projects/             # All your projects live here
│   └── example-project/  # Template showing how it works
│       ├── PROJECT/      # Project management files
│       │   └── WAITING_ON.md  # Current status ← AI reads this first
│       ├── SESSION/      # Session-specific context
│       └── DOCUMENTS/    # Your actual project files

Key Principles
For AIs:

Guide users through the menu - don't just explain, walk them through it
Read WAITING_ON.md at every session start
Suggest practical applications based on what you learn about the user
Keep all project files within their project directory (never in root)

For Humans:

Type menu anytime you're lost
Each project is completely isolated
The AI remembers everything stored in the files
Start with example-project to learn, then create your own
