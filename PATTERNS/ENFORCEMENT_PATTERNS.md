# Enforcement Patterns

**Purpose:** Document effective AI guidance strategies that ensure reliable results
**Usage:** Apply these patterns to improve AI interaction quality
**Maintenance:** Add new patterns as validated, 750-line limit using FIFO when exceeded

---

## PATTERN 1: Constraint-Based > Role-Based Guidance

### What Works
**Constraint-based:** "You cannot proceed to step 2 without step 1 approval"

**Role-based:** "You are an expert who plans carefully"

### Why It Works
- Constraints create structural gates AI cannot bypass
- Roles rely on AI "choosing" to follow guidance
- AIs optimize around constraints, often ignore aspirational roles

### Implementation
```
Ineffective: "You should read documentation before coding"
Effective: "Step 1 mandatory. Cannot proceed without reading REFERENCE.md"
```

---

## PATTERN 2: Blocking Behavior When Knowledge Missing

### What Works
Force AI to pause execution when knowledge is missing:
- "Search for information OR stop and ask"
- "If file not found, explicitly state this and ask for guidance"
- "Cannot proceed without specific evidence"

### Why It Works
- Prevents hallucination (AI can't invent answers)
- Forces explicit uncertainty acknowledgment
- Makes knowledge gaps visible to users

### Implementation
```
When documentation needed:
"AI MUST search project folder for [document-name] OR stop and ask.
DO NOT use general knowledge to guess document content."
```

---

## PATTERN 3: Progressive Coaching Model

### What Works
**First mistake:** Coach with context
- Explain what was missed
- Explain WHY it matters
- Give specific correction
- One chance to learn

**Second mistake (same pattern):** Warning
- Document pattern failure
- Explicit warning about consequences

**Third mistake (same pattern):** Change approach
- Try different methodology
- Consider using different techniques
- Reassess requirements

### Why It Works
- Distinguishes learning (correctable) from systematic issues
- Prevents wasted time on ineffective approaches
- Creates clear improvement path

### Implementation
```
Tracking pattern:
Mistake 1: Coaching ("The API parameter should be 'user_id', not 'id'")
Mistake 2: Warning ("Parameter name error repeated. This pattern suggests a misunderstanding")
Mistake 3: Approach change ("Let's try a different implementation method")
```

---

## PATTERN 4: Checkpoint Gates

### What Works
Mandatory checkpoints between phases:
- Phase 1 → Phase 2: Approval required
- Phase 2 → Phase 3: Evidence required (working code)
- Phase 3 → Phase 4: Testing complete

### Why It Works
- Forces sequential execution (no skipping steps)
- Creates verification points
- Enables early error detection

### Implementation
```
Phase 1 Checkpoint:
- Requirements gathered
- Documentation reviewed
- Approach confirmed
- User approval obtained

Cannot proceed to Phase 2 without APPROVED ✅
```

---

## PATTERN 5: Evidence Requirements

### What Works
Demand proof for every claim:
- "Tests passing" → Screenshot of test output
- "Feature working" → Browser test with steps
- "Documentation updated" → Link to file

### Why It Works
- Prevents "it should work" assumptions
- Forces actual testing
- Creates verification trail

### Implementation
```
AVOID: "Feature should work now"
REQUIRE: "Tested in browser:
1. Clicked login button
2. Entered credentials  
3. Redirected to dashboard
Screenshot attached: [link]"
```

---

## PATTERN 6: Requirements Before Implementation

### What Works
Cannot start implementation without requirements phase:
- Read documentation
- Create checklist
- Confirm understanding
- Get approval

### Why It Works
- Prevents incorrect assumptions
- Catches design issues early
- Forces thinking before acting

### Implementation
```
Requirements Phase:
1. Read REFERENCE.md (mandatory)
2. Read COMMON_MISTAKES.md (mandatory)
3. Create task checklist (quality indicator)
4. Confirm design constraints
5. Get user approval ✅

Zero tolerance for skipping requirements.
```

---

## PATTERN 7: Time Boxing to Prevent Loops

### What Works
Hard time limits:
- 15 minutes on one approach → Try alternative
- 30 minutes stuck → Change strategy
- 2 hours total → Consider session break

### Why It Works
- AI doesn't self-detect being "stuck"
- Prevents circular reasoning
- Forces fresh approaches

### Implementation
```
Session Timing:
0-15 min: Try primary approach
15 min mark: If not working, try alternative approach
30 min mark: If still stuck, fundamentally rethink strategy
2 hour mark: Consider project handover or session break
```

---

## PATTERN 8: Explicit Reasoning Documentation

### What Works
AI must document reasoning at decision points:
- "Using approach X because of constraint Y"
- "This might violate principle Z. Checking before proceeding."
- "Unsure of this design choice. Requesting confirmation."

### Why It Works
- Makes decision process visible
- Enables real-time correction
- Creates traceable logic

### Implementation
```
At design decisions:
"Using microservice architecture because:
1. Data independence requirement
2. Separate scaling needs
3. Team separation mentioned in requirements"
```

---

## PATTERN 9: Early Quality Assessment

### What Works
Quality of early deliverables predicts session success:
- **Good requirements** = Likely competent work
- **Poor requirements** = Likely problematic work
- **Good test design** = Likely thorough implementation
- **Poor test design** = Likely incomplete implementation

### Why It Works
- Fundamental understanding issues reveal themselves early
- Can redirect before significant work is wasted
- Initial quality strongly correlates with final quality

### Implementation
```
Requirements Document Assessment:

High quality indicators:
- Specific, measurable requirements
- Edge cases addressed
- Dependencies identified
- Constraints acknowledged

Low quality indicators:
- Vague requirements
- Missing critical elements
- Contradictory statements
- Over-simplification

Poor quality → Reassess approach early
```

---

## PATTERN 10: Documentation Integration

### What Works
Make documentation part of the deliverable:
- Test plan required
- Usage documentation required
- Implementation notes required
- Examples required

### Why It Works
- Forces thinking about usability
- Creates self-contained deliverables
- Prevents knowledge gaps

### Implementation
```
Completion Checklist:
□ Implementation complete
□ Tests passing
□ Usage documentation added
□ Example added
□ Edge cases documented

Cannot mark complete without all checked.
```

---

## HOW TO ADD NEW ENFORCEMENT PATTERNS

When you discover a reliable enforcement pattern:

1. **Validate it** works across multiple interactions
2. **Document the pattern** using this format
3. **Test with different AIs** to verify transferability
4. **Add examples** showing implementation

```markdown
## PATTERN X: [Descriptive Name]

### What Works
[Specific technique]

### Why It Works
[Explanation of effectiveness]

### Implementation
[Example implementation]
```

Over time, your collection of enforcement patterns will create more predictable AI interactions.

---

**Note for Repository Users:**
This file contains starter enforcement patterns. For optimal results:

1. Add patterns you discover with your specific AI tools
2. Document both successful and unsuccessful approaches
3. Test patterns across different AI models when possible
4. Share effective patterns with your team

Building a shared library of enforcement patterns creates consistent, high-quality AI interactions across your organization.

---

**Last Updated:** [YYYY-MM-DD]  
**Current Patterns:** 10
