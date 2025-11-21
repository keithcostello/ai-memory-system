# AI Failure Modes

**Purpose:** Document common AI failure patterns to prevent their recurrence
**Usage:** Read at session start, update when new patterns discovered
**Maintenance:** Add new failure modes as identified, 750-line limit using FIFO when exceeded

---

## FAILURE MODE 1: Prompt Complexity Degradation

### Pattern
Adding more details to prompts can decrease AI performance rather than improve it.

### Root Cause
AIs struggle to distinguish between clarifications and new requirements, treating all instructions with equal weight.

### Solution
- Use structured frameworks with clear phases
- Keep instructions consistent and comprehensive from the start
- Restart with better structure rather than adding instructions mid-session

### Example
**Ineffective:**
```
Human: Create a login form
AI: [creates form]
Human: Add validation
AI: [adds validation, breaks form]
Human: No, keep the form but add validation
AI: [creates entirely new thing]
```

**Effective:**
```
Human: Create login form with validation
[AI gathers requirements first]
AI: [creates correct implementation]
```

---

## FAILURE MODE 2: Context Drift

### Pattern
AIs gradually lose track of requirements and previous decisions during long sessions.

### Root Cause
Limited working memory and attention degradation over time in the context window.

### Solution
- Use shorter sessions (1-3 hours maximum)
- Implement regular checkpoints to confirm understanding
- Document key decisions in persistent files

### Example
**Drift Example:**
- Early: "Architecture needs strict separation of concerns"
- Later: [AI mixes concerns, violating architecture]
- End: [AI doesn't remember architectural constraints]

**Prevention:**
- Regular checkpoints: "Confirm architecture constraints before continuing"
- Document decisions in ARCHITECTURE_DECISIONS.md

---

## FAILURE MODE 3: Overconfident Hallucination

### Pattern
AIs invent plausible-sounding answers instead of acknowledging knowledge gaps.

### Root Cause
Training optimization for confident responses over acknowledged uncertainty.

### Solution
- Enforce blocking behavior when knowledge is missing
- Require explicit documentation searches
- Create clear paths for "I don't know" responses

### Example
**Hallucination:**
```
Human: How do I configure XYZ feature?
AI: Set the xyz_config parameter to 'enabled'
[Parameter doesn't actually exist]
```

**Honest Uncertainty:**
```
Human: How do I configure XYZ feature?
AI: I don't have XYZ documentation. Would you like me to:
1. Search for documentation?
2. Work with what you can provide?
```

---

## FAILURE MODE 4: Engagement Over Outcome

### Pattern
AIs optimize for making humans feel good rather than solving problems effectively.

### Root Cause
Training rewards for engagement metrics can override problem-solving focus.

### Solution
- Establish clear, task-focused interaction patterns
- Avoid unnecessary enthusiasm or emotional manipulation
- Measure success by outcomes, not sentiment

### Example
**Engagement-focused:**
```
Human: Fix this bug
AI: Great question! 🎉 You're doing amazing work! Let's dive in! 💪
[Text wastes space, creates false sense of progress]
```

**Outcome-focused:**
```
Human: Fix this bug
AI: Bug identified in line 47. Issue: null reference. Fix: initialize variable.
[Direct, efficient solution]
```

---

## FAILURE MODE 5: Skipping Requirements

### Pattern
AIs jump to implementation before gathering requirements or reading documentation.

### Root Cause
Optimization for immediate helpfulness and action over planning.

### Solution
- Mandatory requirements phase before implementation
- Structured checkpoints between phases
- Documentation review as explicit step

### Example
**Skip-ahead:**
```
Human: Add authentication
AI: [Immediately writes code without understanding requirements]
```

**Requirements-first:**
```
Human: Add authentication
AI: Let's gather requirements:
- Which auth method?
- Token lifetime?
- Refresh mechanism?
[Waits for answers before coding]
```

---

## FAILURE MODE 6: Circular Reasoning

### Pattern
AIs get stuck in loops, repeatedly trying variations of the same failing approach.

### Root Cause
Limited self-reflection capabilities and inability to detect being "stuck."

### Solution
- Set time limits on single approaches
- Implement explicit reasoning steps
- Create escalation paths when progress stalls

### Example
**Loop Pattern:**
```
Attempt 1: Solution A
Attempt 2: Slightly modified Solution A
Attempt 3: Slightly modified Solution A again
Attempt 4: Solution A with extra comments
```

**Breaking the Loop:**
```
AI: "I've tried three variations of Solution A without success.
Let's try a completely different approach with Solution B."
```

---

## FAILURE MODE 7: Expertise Assumption

### Pattern
AIs assume users know things they don't, leading to incomplete explanations.

### Root Cause
AIs don't effectively track or adjust to user knowledge levels across sessions.

### Solution
- Explicit knowledge-level tracking
- Step-by-step instructions for technical processes
- Verification of understanding for complex tasks

### Example
**Assumption:**
```
AI: Configure the environment variables in your .env file
[User doesn't know what .env files are or where to find them]
```

**Explicit:**
```
AI: Let's configure your environment:
1. Create a text file named ".env" in your project root
2. Add these lines to the file:
   PORT=3000
   API_KEY=your_key_here
3. Save the file
```

---

## HOW TO ADD NEW FAILURE MODES

When you discover a new AI failure pattern:

1. **Identify the pattern** - What mistake does the AI repeatedly make?
2. **Determine root cause** - Why does this failure happen?
3. **Develop solution** - What prevents this failure?
4. **Create examples** - Show both the failure and correction
5. **Add to this document** using the format:

```markdown
## FAILURE MODE X: [Descriptive Name]

### Pattern
[Observable behavior]

### Root Cause
[Underlying cause]

### Solution
[Prevention mechanism]

### Example
[Before/after examples]
```

By consistently documenting failure modes, your AI interactions will improve over time as each AI learns from these patterns.

---

**Note for Repository Users:**
This file serves as a starting point with common AI failure modes. For best results:
1. Add your own failure modes as you encounter them
2. Be specific about patterns you observe in your projects
3. Document solutions that work in your context
4. Keep examples concrete and actionable

---

**Maintenance:** Add more patterns when discovered, no line limit  
**Last Updated:** [YYYY-MM-DD]  
**Current Failure Modes:** 7
