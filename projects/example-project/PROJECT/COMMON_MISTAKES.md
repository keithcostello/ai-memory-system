# Common Mistakes - Example Project

**Project:** Example Project (Template for new projects)
**Purpose:** YOUR working memory of mistakes to avoid on THIS project. Update actively during sessions.
**Usage:**
- **Session Start:** Read to avoid repeating mistakes
- **During Work:** ADD new mistakes as discovered
- **During Work:** REMOVE outdated/irrelevant items
- **During Work:** UPDATE items with new insights
**Maintenance:** Keep concise - this is YOUR brain, not history dump
**Max Size Target:** <500 lines (if larger, archive old items and keep recent/relevant using FIFO)

---

## MEMORY INDEX - SCAN BEFORE ACTION

**How to Use:** Before performing any action below, scan the listed patterns. P1 items are MANDATORY gates - must verify compliance before proceeding.

### P1 - MANDATORY GATES (Must Check Before Action)

**BEFORE ANSWERING ANY QUESTION:**
→ Pattern 1: Evidence-Based Responses (GATE: Verify facts before responding, no speculation)
→ Pattern 2: Checklist Enforcement (GATE: Run checklist before responding at 50%+ token usage)

**BEFORE SIMULATING EXAMPLES:**
→ Pattern 3: Mark Simulations (GATE: Use <SIMULATION> tag at top when demonstrating examples)

**BEFORE STARTING ANY SPRINT:**
→ Pattern 4: No Sprint Without UAT (GATE: UAT document must exist before coding starts)
→ Pattern 5: Task Breakdown Required (GATE: Cannot estimate without breaking into subtasks)

**BEFORE APPROVING CHECKPOINTS:**
→ Pattern 6: Evidence Required (GATE: No approval without screenshots/test results/file contents)
→ Pattern 7: Test Unhappy Paths (GATE: UAT must include negative test cases)

**BEFORE CODING FEATURES:**
→ Pattern 8: Architecture Validation First (GATE: Architecture validation before feature work)
→ Pattern 9: Tests Before Code (GATE: TDD discipline, no code without test plan)

### P2 - CRITICAL CONTEXT (Should Check for Related Work)

**WHEN STARTING NEW SESSION:**
→ Pattern 10: Session Context Verification (verify memory context is loaded)
→ Pattern 11: Never Assume AI Remembers (check persistent memory loaded)

**WHEN DOCUMENTING:**
→ Pattern 12: Document "Why" Decisions (ARCHITECTURE_DECISIONS.md for non-obvious choices)

**WHEN HANDLING ERRORS:**
→ Pattern 13: Error Handling Not Optional (mandatory before feature complete)

**WHEN SESSION >50% TOKENS:**
→ Pattern 14: Context Window Fatigue Prevention (re-read key documents at checkpoints)

### P3 - GENERAL GUIDANCE (Background Context)

**RECOVERY PATTERNS:**
→ Pattern 15: Document failures immediately (prevents recurrence)
→ Pattern 16: Evidence eliminates assumptions (checkpoint approvals require proof)

---

## FOUNDATIONAL PRINCIPLE

### Evidence-Based Execution

**The Easy AI Path (WRONG):**
- Trust AI claims without verification
- Approve checkpoints based on "looks good"
- Assume tests passing means feature works
- Accept vague responses ("should work now")

**The Right AI Path (CORRECT):**
- Require screenshots, test results, file contents
- Explicit approval language: "APPROVED with evidence: [specifics]"
- Test both happy and unhappy paths
- Demand concrete proof before proceeding

**Why This Matters:**
Every mistake in this document stems from accepting claims without evidence. Architecture violations, skipped tests, missing documentation - all preventable with evidence requirements.

**The Discipline:**
Before approving ANY checkpoint:
1. **Require evidence:** What can I see/verify to confirm this?
2. **Check completeness:** Did they test edge cases?
3. **Validate claims:** Do the test results actually prove what they claim?
4. **Document proof:** Include evidence in approval message

---

## Communication Mistakes

### Pattern 3: Mark Simulations Clearly
- ❌ Simulating examples without clear marking (confuses real vs demo)
- ✅ Use <SIMULATION> tag at top of any example/demonstration
- **Why:** Helps maintain clear context boundaries between real work vs examples

### Pattern 11: Never Assume AI Remembers
- ❌ Starting new session expecting AI to have context
- ✅ Use persistent memory system, verify loaded
- **Why:** Prevents wasted time repeating explanations without memory system

---

## Sprint Execution Mistakes

### Pattern 4: No Sprint Without UAT
- ❌ Starting coding without defining success criteria
- ✅ Create UAT document before sprint starts, zero exceptions
- **Why:** Prevents building wrong features when success is undefined

### Pattern 8: Architecture Validation Before Features
- ❌ Building features before architecture validation
- ✅ Mandatory architecture review checkpoint before feature work
- **Why:** Prevents refactoring and wasted work after implementation

### Pattern 9: Tests Before Code (TDD)
- ❌ Writing implementation first, tests second
- ✅ Tests first, always. No exceptions.
- **Why:** Ensures tests actually validate requirements, not just implementation

---

## Planning Mistakes

### Pattern 5: Task Breakdown Required
- ❌ Estimating without breaking down into subtasks
- ✅ Mandatory task breakdown before sprint start
- **Why:** Prevents underestimation of complex tasks

---

## Validation Mistakes

### Pattern 6: Evidence Required for Approval
- ❌ AI says "looks good" without proof
- ✅ "APPROVED with evidence: [specific outcomes]"
- **Why:** Prevents approval of incomplete or non-functional work

### Pattern 7: Test Unhappy Paths
- ❌ Testing only happy path scenarios
- ✅ UAT must include negative test cases and edge conditions
- **Why:** Prevents production failures from untested edge cases

---

## Documentation Mistakes

### Pattern 12: Document "Why" Decisions
- ❌ Writing code without explaining non-obvious choices
- ✅ ARCHITECTURE_DECISIONS.md for every significant decision
- **Why:** Prevents uncertainty when modifying code later

### Pattern 13: Error Handling Not Optional
- ❌ Shipping features without error handling "for now"
- ✅ Mandatory error handling before feature complete
- **Why:** Ensures error handling is implemented before release

---

## Recovery Patterns (What Worked)

### Pattern 15: Document Failures Immediately
- **What works:** Capture every mistake as it happens
- **Result:** Prevents repeating the same mistakes
- **Lesson:** Real-time documentation prevents recurrence

### Pattern 16: Evidence Eliminates Assumptions
- **What works:** Require screenshots, test results, and file contents
- **Result:** Approve only when evidence proves completion
- **Lesson:** Evidence-based approval prevents bad work

---

## Current Active Patterns

**Working Well (Keep enforcing):**
- ✅ Checkpoint discipline
- ✅ Task breakdown before coding
- ✅ UAT gates
- ✅ Evidence requirements
- ✅ <SIMULATION> tag usage

**Needs Active Enforcement (Add your own):**
- ⚠️ [Your pattern here]
- ⚠️ [Your pattern here]

**Needs Improvement (Add your own):**
- ⚠️ [Your area for improvement]
- ⚠️ [Your area for improvement]

---

## Metadata

**Last Updated:** [YYYY-MM-DD] (Session [X])
**Total Mistakes Documented:** [Number]
**Source Sessions:** [List sessions]
**Archive Policy:** When file exceeds 500 lines, move oldest P2/P3 to ARCHIVE/

**Lines:** [current]/500
