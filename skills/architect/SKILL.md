---
name: architect
description: Design types, function signatures, and module structure before writing code, then implement against that design. Use for "architect this", "design this", or non-trivial work where jumping straight to code could lock in the wrong shape.
argument-hint: "[feature or change to design]"
---

# Architect

Design $ARGUMENTS before writing real code. **Never** push, commit, comment, or post anywhere.

## 1. Understand what exists

Run the **how** skill on every part of the system the new code touches. If the design changes who owns what, also run the **why** skill so the existing reasons become constraints, not guesses. Skip this only for truly new code with nothing to connect to.

## 2. Sketch at least two designs

Write each design as code skeletons only: types, interfaces, function signatures, module boundaries. Bodies are `throw new Error("not implemented")` or short pseudocode comments.

The designs must be structurally different (different module split, data model, or ownership), not small variations of one idea.

## 3. Check each design for red flags

- **Shallow module**: a big interface that hides little. Callers must call several methods in order to do one thing.
- **Leaking details**: the same internal decision (a storage schema, wire format, framework type) shows up in several modules, so one change needs edits in many places.
- **Split by time, not knowledge**: separate load / validate / transform / save modules that all repeat the same data shape and rules.
- **Pass-through**: methods that only forward to another method with the same signature.
- **Easy to misuse**: a change that looks right from one file would be wrong for the whole system.

Prefer the design that hides the most complexity behind the smallest, simplest public interface.

## 4. Agree

Show the chosen design: the skeletons, why it won, and what the other design would have been better at. **Wait for the user's OK** before implementing, unless they said to go straight ahead.

## 5. Implement against the sketch

Replace the stubs with real code. The sketch is the contract. If you need something the sketch didn't plan for (an extra parameter, a new dependency), stop and say so: the sketch was wrong, a requirement was missed, or the code is doing too much. Update the sketch when the user accepts a change.

## 6. Scrap it when the design is wrong

Signs it's wrong (a pattern, not one case):
- The same kind of workaround keeps appearing in unrelated places.
- Many unrelated edge cases each need their own special-case branch.
- Types need `any`, casts, or always-set optional fields to compile.
- Callers must know the module's internals to use it.

When that happens, don't patch. Say so, re-run **how** on what's built, and redesign as if the new constraints were known from day one.
