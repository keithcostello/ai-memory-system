# Standard Handoff Template (8 Sections)

This template provides a streamlined 8-section handoff specifically designed for the memory-repo repository. It balances thoroughness with simplicity, focusing on critical information for session continuity.

## Handoff Format

```markdown
# AI Handoff: memory-repo

## VALIDATION CHECKLIST
**IMPORTANT: Receiving AI must answer these before proceeding.**

1. What is the primary task you need to continue?
2. Which file should you read first?
3. What's the current blocker or challenge (if any)?

## ESSENTIAL FILES (READ IN THIS ORDER)
1. `[path/to/primary/file]` - [critical context]
2. `[path/to/secondary/file]` - [why needed]
3. [additional files in priority order]

## NEXT ACTIONS
1. [Specific next task with clear success criteria]
2. [Second task with any specific instructions]
3. [Additional tasks in priority order]

## KNOWN ISSUES/BLOCKERS
* [Current blocker and status]
* [Edge case to be aware of]
* [Limitation that affects work]

## PROJECT CONTEXT
Brief overview of the project (2-3 sentences)

## CURRENT STATUS
* **Phase:** [Design/Implementation/Testing/etc.]
* **Progress:** [%] complete
* **Last Activity:** [Brief description of last completed task]

## KEY DECISIONS
* **Decision 1:** [Brief explanation] → See `[file reference]`
* **Decision 2:** [Brief explanation with file reference]

## TIPS FOR NEXT SESSION
* [Important reminder or guidance]
* [Areas to be careful with]
* [Suggestion on approach]
```

## Implementation Guidelines

### For the Handoff Creator

1. **Essential Files Section:**
   - Prioritize by reading importance
   - Include brief reason WHY each file should be read
   - Maximum 5 files (focus on the most critical ones)

2. **Validation Questions:**
   - Questions should be answerable ONLY by reading the handoff
   - Focus on next actions and critical context

3. **Avoid Duplication:**
   - Don't copy large sections from PROJECT files
   - Use links/references to existing documentation

### For the Handoff Recipient

1. **Verification First:**
   - Answer validation questions before proceeding
   - If you can't answer, reread handoff carefully

2. **File Reading Order:**
   - Follow the exact reading order specified

3. **Acknowledge Reception:**
   - Confirm receipt of handoff in next session

## Example for memory-repo Project

```markdown
# AI Handoff: memory-repo

## VALIDATION CHECKLIST
1. What file format should you use for chat folders? (YYYYMMDD-HHMMSS_name)
2. Which file should you read first? (WAITING_ON.md)
3. What's the primary next action? (Fix uppercase PROJECTS directory)

## ESSENTIAL FILES (READ IN THIS ORDER)
1. `projects/example-project/PROJECT/WAITING_ON.md` - Current status and next actions
2. `PERSISTENT_MEMORY_LITE.md` - System design principles
3. `memory-repo/README.md` - Implementation structure

## NEXT ACTIONS
1. Fix directory case sensitivity issue (PROJECTS → projects)
2. Ensure example-project has proper README.md
3. Validate all file references are correct

## KNOWN ISSUES/BLOCKERS
* Case sensitivity in PROJECTS directory causes path resolution issues
* Some file paths in documentation reference incorrect structure

## PROJECT CONTEXT
GitHub-based memory system providing persistent context across AI sessions with three-tier storage architecture and project isolation.

## CURRENT STATUS
* **Phase:** Implementation
* **Progress:** 60% complete
* **Last Activity:** Created PROJECT_ISOLATION_RULES.md

## KEY DECISIONS
* **Directory Structure:** `projects/[name]/{PROJECT,SESSION,DOCUMENTS}` for three-tier storage
* **Chat Folders:** Timestamp format `YYYYMMDD-HHMMSS_name` for consistent organization

## TIPS FOR NEXT SESSION
* Remember to validate paths after renaming PROJECTS → projects
* Test all reference links after structure changes
* Update any absolute paths to relative
```

## Storage Location

Store handoffs in the project's SESSION directory using timestamp format: `YYYYMMDD-HHMMSS_handoff.md`

## Reference in WAITING_ON.md

Always reference the handoff in WAITING_ON.md:

```markdown
**Handoff:** SESSION/YYYYMMDD-HHMMSS_handoff.md created for next session
```

This ensures the next AI knows where to find the handoff document.