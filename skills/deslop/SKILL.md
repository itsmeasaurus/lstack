---
name: deslop
description: Remove typical AI-written code clutter from the current branch's changes, such as needless comments, over-defensive checks, any-casts, and deep nesting. Use for "deslop", "clean up AI code", or "remove slop".
argument-hint: "[base branch, optional]"
---

# Deslop

Clean up AI-style clutter that **this branch added**. Compare against the base: $ARGUMENTS if given, otherwise the default branch (`git diff <base>...HEAD` plus uncommitted changes). Never commit, push, or post anywhere.

## Remove or fix

- Comments that just repeat what the code says, or that don't match the file's usual comment style.
- `try/catch` blocks and defensive checks that are unusual for trusted internal code (input is already validated at the edge).
- `as any` or other casts used only to silence the type checker.
- Deep nesting that early returns would flatten.
- Anything else that doesn't match the style of the file and the code around it: naming, logging, error format, helper usage.

## Rules

- Keep behavior the same, unless you find a clear bug. Report any bug separately instead of quietly fixing it.
- Small, focused edits. No broad rewrites.
- Only touch lines this branch added or changed.

## Report

One to three sentences on what you cleaned up.
