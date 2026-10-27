---
name: ci-fix
description: Find why the pull request's CI checks are failing and fix the code locally, without committing or pushing. Use for "CI is failing", "fix the build", or "why are checks red".
argument-hint: "[PR number, optional]"
allowed-tools: Read Grep Glob Bash(gh pr view *) Bash(gh pr checks *) Bash(gh run view *) Bash(gh run list *) Bash(git status *) Bash(git diff *)
---

# CI fix (local only)

Find why CI is failing and fix it in the local working tree. **Never** commit, push, re-run CI, comment, or post anything. The user reviews and pushes the fix.

1. Find the PR: $ARGUMENTS if given, otherwise the current branch's PR.
2. List checks: `gh pr checks <n> --json name,state,bucket,workflow,link`.
3. For each failed job, read the log with `gh run view <run-id> --log-failed`. Find the **first** real error, not the follow-on noise. If the check isn't a GitHub Action, use its link to name the failing command or service.
4. Reproduce it locally by running the same command (for example the test, lint, or build script from `package.json`) when that's possible. Ask before running anything slow or that needs network access or secrets.
5. Apply the smallest safe fix. One failure at a time. Prefer small, low-risk changes over refactors.
6. Re-run the failing command locally to confirm it passes.

## Report

- The failing job and its root error.
- What you changed, file by file (`git diff` summary).
- Local result after the fix.
- What the user should do next (review, commit, push), and any failure you could not reproduce locally.
