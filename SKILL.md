---
name: clean-break-context-packing
description: A 60-second end-of-shift protocol that cleanly freezes working state, commits checkpoints, stashes uncommitted experiments, and writes a crisp continuation line. Ensures any incoming AI model or human operator can orient in under 30 seconds with zero context degradation.
license: MIT
metadata:
  author: We Build for Good
  version: "1.0.0"
---

# Clean Break & Context Packing Protocol

In autonomous and pair-programming AI workflows, sessions rarely end at convenient times. 

A session abruptly cuts off due to token window exhaustion, rate limits, network drops, or the human operator closing their laptop to sleep.

When an AI crashes mid-sentence, it leaves behind:
* Uncommitted files scattered across the working tree.
* Half-written functions that break local builds.
* Zero notes explaining what was being attempted.

The next AI session (or the human engineer) spends thirty minutes reconstructing what was happening, frequently throwing away good work by mistake.

The `clean-break-context-packing` protocol provides a structured 60-second procedure to cleanly freeze working state whenever an AI senses session completion, context exhaustion, or an end-of-shift handoff.

---

## The Prime Philosophy

**Never leave a messy campsite. Leave a clean branch, a passing checkpoint, and a single obvious next step.**

Any successor (whether human or an incoming AI model) should be able to sit in the chair and begin productive work within thirty seconds.

---

## The 60-Second Clean Break Sequence

When reaching the end of a shift, an approaching token threshold, or when asked to "wrap up":

### Step 1: Freeze the Line
* Stop starting new features or refactorings.
* Wrap the current file edit to a syntactically valid state.

### Step 2: Commit the Checkpoint
* Stage and commit all working changes to the active branch.
* Use a clear, descriptive commit message:
  * If complete: `feat(scope): implement target behavior`
  * If mid-flight: `wip(scope): checkpoint before session handoff - tests passing`
* Never leave uncommitted files dirty in the working tree unless explicitly stashed with a named label (`git stash push -m "wip-experiment"`).

### Step 3: Verify the Tree
* Run `git status --short`.
* Confirm the working tree is clean.

### Step 4: Write the 3-Line Continuation Pointer
* Append or update the project's continuation file (e.g. `CONTINUE.md` or session handoff log) with exactly three lines:
  1. **Ground Truth**: Branch name and head commit hash.
  2. **Last Verified State**: What command was run and verified green.
  3. **Immediate Next Step**: The exact file, function, and action for the next turn.

---

## Canonical Continuation Pointer Example

```markdown
### Continuation Pointer
- **Branch & Head**: `fix/checkout-tax-calc` @ `a4c90e2` (Working tree clean)
- **Verified State**: `pnpm test tests/tax.test.ts` passed (8/8 green)
- **Next Turn Action**: Open `src/checkout/ReviewStep.tsx` line 84 and wire `calculatedTax` to the subtotal summary.
```

---

## The Wake-Up Test

An orientation passes the Clean Break test if:
* The incoming developer or AI can run `git status` and find a clean tree.
* The incoming developer can read the continuation pointer and execute the next command immediately without asking "What were you working on?"
