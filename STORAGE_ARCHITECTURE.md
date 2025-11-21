# Three-Tier Storage Architecture Diagram

```
┌───────────────────────────────────────────────────────────┐
│                                                           │
│  COLD STORAGE (PATTERNS/)                                 │
│  ═══════════════════════                                  │
│                                                           │
│  • Repository-wide knowledge and patterns                 │
│  • Rarely changes, high stability                         │
│  • 750-line limits per file                               │
│                                                           │
│  Files:                                                   │
│  - VALIDATED_APPROACHES.md                                │
│  - ENFORCEMENT_PATTERNS.md                                │
│  - AI_FAILURE_MODES.md                                    │
│                                                           │
└───────────────────────────────────────────────────────────┘
                          ▲
                          │
                          │ References
                          │
                          ▼
┌───────────────────────────────────────────────────────────┐
│                                                           │
│  WARM STORAGE (projects/*/PROJECT/)                       │
│  ═══════════════════════════════                          │
│                                                           │
│  • Project-specific information                           │
│  • Changes frequently, but not every session              │
│  • 500-line FIFO maintenance per file                     │
│                                                           │
│  Files:                                                   │
│  - WAITING_ON.md                                          │
│  - COMMON_MISTAKES.md                                     │
│  - ARCHITECTURE_DECISIONS.md                              │
│                                                           │
└───────────────────────────────────────────────────────────┘
                          ▲
                          │
                          │ References
                          │
                          ▼
┌───────────────────────────────────────────────────────────┐
│                                                           │
│  HOT STORAGE (projects/*/SESSION/)                        │
│  ══════════════════════════════                           │
│                                                           │
│  • Session-specific context                               │
│  • Changes every session                                  │
│  • 500-line FIFO maintenance for SESSION_LOG.md           │
│  • 100-line target for CURRENT_CONTEXT.md                 │
│                                                           │
│  Files:                                                   │
│  - CURRENT_CONTEXT.md                                     │
│  - SESSION_LOG.md                                         │
│  - YYYYMMDD-HHMMSS_*/chat.log (750-line limit)            │
│                                                           │
└───────────────────────────────────────────────────────────┘

```

## Information Flow

1. **Initial Setup:**
   - PATTERNS/ directory contains repository-wide knowledge (Cold Storage)
   - Projects have their own isolated directory structure

2. **Project-Level Work:**
   - PROJECT/ files track status and decisions (Warm Storage)
   - FIFO maintenance keeps files at 500-line limit

3. **Active Sessions:**
   - SESSION/ files track current context (Hot Storage)
   - Timestamp-based chat folders organize conversations
   - CURRENT_CONTEXT.md is continually updated

4. **Memory Refreshes:**
   - AI reads from all three tiers in sequence:
     1. Cold storage (patterns)
     2. Warm storage (project context)
     3. Hot storage (current context)

5. **File Maintenance Path:**
   - When files reach limits:
     - Create ARCHIVE/ directory if needed
     - Move oldest entries to dated archive files
     - Keep most recent/relevant information in main file

## Advantages of Three-Tier Architecture

- **Scalability:** System handles multiple projects without performance degradation
- **Isolation:** Projects remain completely independent
- **Maintenance:** Each tier has appropriate update frequency
- **Retrieval:** AI can efficiently access information at the right tier
- **Persistence:** Knowledge is retained at appropriate levels of permanence