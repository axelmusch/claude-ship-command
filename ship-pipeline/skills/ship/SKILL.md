---
name: ship
description: Plan -> implement -> test -> review, looping until the review passes. Invoke manually with the requirement as the argument.
argument-hint: [requirement]
allowed-tools: Task, Read, Write, Bash
disable-model-invocation: true
---
Build the following requirement end to end: $ARGUMENTS

Run this pipeline. Each stage is a subagent; hand off via files in
`.claude/workflow/`. Do the stages in order and DO NOT skip the review.

1. Delegate to the **ship-planner** subagent with the requirement above.
2. Delegate to the **ship-implementer** subagent.
3. Delegate to the **ship-tester** subagent.
4. Delegate to the **ship-reviewer** subagent.
5. Read `.claude/workflow/review.md`:
   - If it contains `VERDICT: PASS`, stop and report success with a short
     summary of what was built.
   - If it contains `VERDICT: FAIL`, go back to step 2 (ship-implementer),
     which will read the unmet criteria and fix them, then continue through
     test and review again.
6. Repeat the loop a maximum of 3 times. If still failing after 3 rounds,
   stop and report the remaining unmet criteria — do not keep looping.

Never edit code yourself in this orchestrating turn; all changes go through
the ship-implementer subagent, and all verification through the read-only
ship-reviewer.
