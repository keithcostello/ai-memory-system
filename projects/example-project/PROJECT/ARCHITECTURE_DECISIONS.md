# Project Architecture Decisions

**Purpose:** Record of significant architectural decisions and rationale
**Last Updated:** [YYYY-MM-DD]
**Maintenance:** When file exceeds 500 lines, archive oldest decisions using FIFO

---

## DECISION TEMPLATE (Copy for each new decision)

## DECISION [NUMBER]: [Title of Architecture Decision]

**Date:** [YYYY-MM-DD]
**Status:** [✅ Implemented | ⏳ In Progress | ❌ Rejected | ⌛ On Hold]

**Decision:** [One sentence summary of what was decided]

**Context:**
- [Why is this decision necessary?]
- [What problem does it address?]
- [What constraints exist?]
- [What requirements drove this?]

**Alternatives Considered:**
1. **[Alternative 1]** - [Reason for selection/rejection]
2. **[Alternative 2]** - [Reason for selection/rejection]
3. **[Alternative 3]** - [Reason for selection/rejection]

**Rationale:**
- [Main reason 1 for decision]
- [Main reason 2 for decision]
- [Main reason 3 for decision]
- [How this addresses the context]

**Consequences:**
- ✅ [Positive consequence 1]
- ✅ [Positive consequence 2]
- ⚠️ [Negative/risk consequence 1]
- ⚠️ [Negative/risk consequence 2]

**References:**
- [Link to relevant documentation]
- [Link to requirements]
- [Link to research]

**Would We Change It?** [Yes/No/Maybe] + brief explanation

---

## EXAMPLE DECISION 1: Project Structure

**Date:** [YYYY-MM-DD]
**Status:** ✅ Implemented

**Decision:** Implement a structured project organization with session-based memory system

**Context:**
- Need consistent organization across projects
- Manual context management is error-prone
- Cross-session memory requires structure
- Multiple projects require isolation

**Alternatives Considered:**
1. **Ad-hoc organization** - Rejected (creates inconsistency)
2. **Single file approach** - Rejected (becomes unwieldy)
3. **Complex database solution** - Rejected (overengineering for most projects)

**Rationale:**
- Consistent structure enables faster onboarding
- Session-based organization preserves historical context
- Project isolation prevents cross-contamination
- Simple file-based system is accessible to all

**Consequences:**
- ✅ Clear organization of project information
- ✅ Predictable location for all project artifacts
- ✅ Easy navigation between sessions and projects
- ⚠️ Requires discipline to maintain structure
- ⚠️ Initial setup time investment

**References:**
- PERSISTENT_MEMORY_LITE.md
- projects/example-project/README.md

**Would We Change It?** No. Structure provides significant benefits with minimal overhead.

---

## DECISIONS PENDING

### PENDING 1: [Decision Topic]

**Context:** [Brief description of the pending decision]

**Blocking:** [What information is needed before deciding?]

**Timeline:** [When this decision needs to be made]

### PENDING 2: [Decision Topic]

**Context:** [Brief description of the pending decision]

**Blocking:** [What information is needed before deciding?]

**Timeline:** [When this decision needs to be made]

---

## ARCHITECTURAL PRINCIPLES (Add your project's guiding principles)

1. **[Principle 1]**
   - [Description of principle]
   - [Why it matters]
   - [How to apply it]

2. **[Principle 2]**
   - [Description of principle]
   - [Why it matters]
   - [How to apply it]

3. **[Principle 3]**
   - [Description of principle]
   - [Why it matters]
   - [How to apply it]

---

## HOW TO USE THIS DOCUMENT

### When to Record a Decision

Record an architecture decision when:
1. It affects multiple components
2. It would be expensive to change later
3. It represents a significant technical choice
4. It affects the project's long-term evolution

### How to Document a Decision

1. Copy the DECISION TEMPLATE section
2. Fill in all fields honestly, including alternatives
3. Be specific about the context that led to the decision
4. Document both positive and negative consequences
5. Always include the "Would We Change It?" reflection

### Maintenance Guidelines

1. Keep under 500 lines total (use FIFO for archiving)
2. Update the status of decisions as they evolve
3. Revisit "Would We Change It?" after implementation
4. Move completed PENDING items to full decisions
5. Review document at project milestones

---

**Version:** 1.0
**Next Review:** [Date or milestone]
**Maintained By:** [Names or roles]
