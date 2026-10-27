---
name: tdd
description: Fix a bug by first writing a test that fails because of it, then fixing the code so the test passes. Use when the user asks for TDD, a failing test, or a regression test, or when the bug has an obvious, cheap local test. Skip when testing would be slow, unclear, or need heavy setup.
argument-hint: "[bug to fix]"
---

# TDD bug fix

Fix $ARGUMENTS by making the bug show up in a test before changing the code. Never push or post anywhere.

## Steps

1. **Understand the bug**: what should happen, what happens instead, which code path, and the smallest way to reproduce it.
2. **Pick the closest existing test type** for that code (unit, integration, etc.) and follow how nearby tests are written. Don't build a new test setup from scratch just for this.
3. **Write the failing test first.** Test the intended behavior, not how the code currently works inside.
4. **Run it and confirm it fails for the right reason.** Quote the actual failure message, not just the assertion line. A crash, an empty result, and the predicted mismatch all show red, but only the predicted mismatch proves the test catches the bug. If it passes or fails for another reason, fix the test first.
5. **Fix the code** with the smallest change that gives the intended behavior.
6. **Re-run the test** and confirm it passes. Run the nearby tests too.

## When a test isn't practical

If a test would need broad setup, fragile mocks, slow end-to-end infrastructure, production data, or unclear reproduction steps, don't force it. Use the closest real check instead: a small script, a manual reproduction command, or a focused integration check.

No test is better than a bad test. A bad test mostly tests mocks, copies the implementation, depends on timing, or would be deleted right after.

## Rules

- Never change a test just to match wrong code.
- Never weaken an existing assertion unless the expected behavior truly changed, and say why.
- Keep the test focused on this bug.
- For a flaky bug, make the test deterministic where possible.

## Report

- The test and the failure it showed **before** the fix (quoted, trimmed).
- The passing run **after** the fix, and other tests you ran.
- If you couldn't show a failing test, say why and what you checked instead.
