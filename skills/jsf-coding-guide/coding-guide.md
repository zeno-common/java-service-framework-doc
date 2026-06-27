# CLAUDE.md

Guidelines to reduce LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** Biases toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

- State assumptions explicitly; if unclear or uncertain, stop and ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features, abstractions, or configurability beyond what was asked.
- No error handling for impossible scenarios.
- If 200 lines could be 50, rewrite it.

Test: would a senior engineer call this overcomplicated? If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

- Don't refactor, "improve," or reformat adjacent code.
- Match existing style, even if you'd do it differently.
- Notice unrelated dead code? Mention it - don't delete it.
- Remove only the orphans YOUR changes created.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals. For examples, plan template, and self-verification checklist, see [coding-guide-details.md](coding-guide-details.md).

Strong criteria enable independent looping; weak ones ("make it work") need constant clarification.