# Validated Approaches

**Purpose:** Document successful AI interaction patterns with proven effectiveness
**Usage:** Apply these approaches to improve AI collaboration quality
**Maintenance:** Add new approaches as validated, 750-line limit using FIFO when exceeded

---

## APPROACH 1: Micro-Sessions (1-3 Hours)

### What It Is
Break work into 1-3 hour focused sessions instead of long, continuous interactions.

### Why It Works
- Matches AI attention span limitations
- Prevents context drift
- Enables frequent checkpoints
- Reduces cost per failure

### Implementation
Break features into smallest testable units:
```
Ineffective: "Build entire authentication system" (8+ hours)
Effective: "Add token generation" (1 hour)
          "Add token validation" (1 hour)
          "Add refresh token logic" (1.5 hours)
```

### When to Use
All significant AI development work. Shorter sessions produce better results than marathon sessions.

---

## APPROACH 2: Documentation-First

### What It Is
Create documentation DURING development, not after completion. Make it mandatory for closure.

### Why It Works
- Prevents technical debt accumulation
- Forces thinking about user impact
- Creates clear knowledge record
- Saves time long-term

### Implementation
Project completion requires:
- Test documentation
- Architecture documentation (if changed)
- API documentation updates
- Usage examples

### When to Use
Any complex project. Documentation-first is always more efficient than documentation-after.

---

## APPROACH 3: Repository-Backed Memory

### What It Is
Use a version-controlled repository as persistent memory layer for AI sessions:
- PROJECT/STATUS.md (project status)
- PROJECT/LESSONS.md (project learnings)
- SESSION/LOGS.md (session narrative)

### Why It Works
- Zero context loss between sessions
- Works across different AI tools
- Enables team coordination
- Automatic version control

### Implementation
```
Session Start:
1. Read project status files
2. Load project context
3. Proceed with full understanding

Session End:
1. Update session context
2. Document blockers, decisions, next actions
3. Commit to repository
```

### When to Use
Any multi-session project. Makes sessions stateful rather than starting fresh each time.

---

## APPROACH 4: Multi-Model Compatibility

### What It Is
Design workflows that function across different AI systems, not tied to a specific platform.

### Why It Works
- Prevents vendor lock-in
- Validates fundamental approach effectiveness
- Enables tool switching without rework

### Implementation
Design constraints, not model-specific prompts:
```
Ineffective: "[Model name], you are an expert..." (model-specific role)
Effective: "Phase 1 must complete before Phase 2" (structural constraint)
```

### When to Use
When building reusable systems that need to work with multiple AI platforms.

---

## APPROACH 5: Knowledge Separation (Core vs Details)

### What It Is
Separate fundamental principles (internalize) from implementation details (retrieve as needed).

### Why It Works
- Reduces cognitive overload
- AI retrieves specific procedures only when needed
- Core principles stay consistently applied
- Prevents information overwhelm

### Implementation
```
Core Knowledge (Always Available):
- Key principles
- When to apply approaches
- Fundamental concepts

Retrievable Details:
- Specific implementation steps
- Checklists
- Technical specifications
```

### When to Use
Any complex system with both principles and specific procedures.

---

## APPROACH 6: Constraint-Based Direction

### What It Is
Use structural constraints that AI must follow, rather than behavioral suggestions.

### Why It Works
- Constraints create non-optional boundaries
- Suggestions can be ignored when inconvenient
- AIs naturally optimize within constraints

### Implementation
```
Ineffective: "Try to document your code well"
Effective: "Each function requires documentation before proceeding"
          "Tests must pass before review"
```

### When to Use
Whenever consistent, high-quality output is required.

---

## APPROACH 7: Blocking on Uncertainty

### What It Is
Require AI to pause and request information when knowledge is missing, rather than guessing.

### Why It Works
- Prevents inaccurate assumptions
- Forces explicit uncertainty acknowledgment
- Makes knowledge gaps visible
- Creates opportunity for correction

### Implementation
```
Knowledge Requirement:
"AI must verify [information] exists before proceeding.
If information is missing, STOP and request it.
DO NOT proceed with incomplete information."

When blocked:
"Missing [specific information]. Options:
1. Can you provide this information?
2. Should I search for alternatives?
3. Should I make an educated guess (not recommended)?"
```

### When to Use
Any scenario where accuracy matters more than continuous flow.

---

## APPROACH 8: Progressive Response Protocol

### What It Is
Implement a structured coaching system with clear escalation paths.

### Why It Works
- Distinguishes correctible issues from systematic problems
- Prevents wasted time on ineffective approaches
- Creates measurable improvement path

### Implementation
```
First issue: Provide guidance
- Explain the issue
- Show the correct approach
- Explain reasoning

Second occurrence: Warning
- Note recurring pattern
- Re-explain with more detail
- Flag potential systematic issue

Third occurrence: Change approach
- Acknowledge approach isn't working
- Switch to alternative method
- Document lesson learned
```

### When to Use
Any extended collaboration where improvement matters.

---

## APPROACH 9: Early Detection Signals

### What It Is
Use quality of initial deliverables to predict overall project success likelihood.

### Why It Works
- Fundamental understanding issues reveal themselves early
- Early correction saves significant time
- Initial work quality strongly correlates with final quality

### Implementation
```
Quality Signals:
Good planning document → High success probability
Vague planning document → Low success probability
Good test cases → High success probability
Missing edge cases → Low success probability

Poor early signals → Immediate reassessment required
```

### When to Use
Any project with significant time investment. Check quality signals before deep commitment.

---

## APPROACH 10: User Knowledge Calibration

### What It Is
Test systems with users of varying technical skill levels to ensure broad usability.

### Why It Works
- Validates approach works regardless of user expertise
- Exposes implicit knowledge assumptions
- Improves universal accessibility

### Implementation
```
Multi-level testing protocol:
1. Expert user test
2. Intermediate user test
3. Beginner user test

Success criterion: All user levels can achieve core tasks
```

### When to Use
Any system intended for diverse user bases.

---

## APPROACH 11: Evidence-Based Verification

### What It Is
Require concrete evidence for every significant claim or completion.

### Why It Works
- Prevents "should work" assumptions
- Forces actual verification
- Creates accountability
- Enables independent assessment

### Implementation
```
Claim: "Feature is implemented"
Required Evidence: Screenshot, test results, or runnable code

Claim: "Bug is fixed" 
Required Evidence: Before/after comparison, test case that now passes
```

### When to Use
Any deliverable where verification matters. Never accept claims without evidence.

---

## APPROACH 12: Requirements-First Development

### What It Is
Mandatory requirements phase before implementation:
- Documentation review
- Requirement clarification
- Implementation planning
- Approval checkpoint

### Why It Works
- Prevents incorrect assumptions
- Catches design issues early
- Forces thinking before coding
- Establishes clear success criteria

### Implementation
```
Requirements Phase Checklist:
1. Read all relevant documentation
2. List explicit requirements
3. Identify edge cases and constraints
4. Create implementation plan
5. Get approval before proceeding

No implementation without completed requirements phase.
```

### When to Use
Any non-trivial development task. Always define success before starting.

---

## HOW TO ADD NEW APPROACHES

When you discover a reliable approach:

1. **Test it thoroughly** in multiple contexts
2. **Document both what works AND why** it works
3. **Create clear implementation examples**
4. **Specify when to use the approach**
5. **Add to this document** using the format:

```markdown
## APPROACH X: [Descriptive Name]

### What It Is
[Clear description]

### Why It Works
[Explanation of effectiveness]

### Implementation
[Example implementation]

### When to Use
[Appropriate scenarios]
```

Building a library of validated approaches creates consistent, high-quality AI interactions.

---

**Note for Repository Users:**
This file contains starter approaches that work across multiple AI systems. For best results:

1. Test these approaches in your specific context
2. Document which work best for your particular needs
3. Add new approaches you discover
4. Share effective approaches with your team

Creating an organizational knowledge base of effective approaches dramatically improves AI collaboration quality.

---

**Last Updated:** [YYYY-MM-DD]  
**Current Approaches:** 12
