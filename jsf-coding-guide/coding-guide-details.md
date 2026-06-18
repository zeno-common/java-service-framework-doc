# CLAUDE.md — Details

> On-demand reference for §4 (Goal-Driven Execution). Load when handling multi-step tasks or verifying work.

## Task → Verifiable Goal Transformations

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

## Multi-Step Plan Template

For multi-step tasks, state a brief plan:

```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

## Self-Verification

**Working if:** fewer unnecessary diff changes, fewer rewrites from overcomplication, and clarifying questions come before implementation, not after mistakes.