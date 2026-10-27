---
name: fix-merge-conflicts
description: Resolve merge or rebase conflicts, then check that build, lint, and tests still pass. Leaves the result for the user to commit. Use for "fix the merge conflicts" or "resolve conflicts".
allowed-tools: Read Grep Glob Bash(git status *) Bash(git diff *) Bash(git log *) Bash(git show *)
---

# Fix merge conflicts

Resolve all conflicts so the branch builds again. **Never** commit, continue the merge/rebase, push, or tag. The user does those.

## Steps

1. Find every conflicted file with `git status` and search for leftover conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
2. For each conflict, understand what **both** sides intended (`git log` / `git show` on each side if it's unclear).
3. Resolve with minimal, correctness-first edits:
   - Keep both sides' changes when they can live together.
   - Otherwise choose the version that compiles and keeps public behavior stable, and note it.
4. **Lockfiles** (`package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`): don't hand-edit. Resolve `package.json` first, then ask before running the package manager to regenerate the lockfile, since that downloads from the registry.
5. Confirm no conflict markers remain anywhere.
6. Run the project's build, lint, and relevant tests (from `package.json` scripts). Fix only what the merge broke.
7. Stage the resolved files with `git add`, but do not commit.

## Rules

- No refactoring while resolving.
- If a conflict needs a product decision (both sides changed behavior on purpose), stop and ask.

## Report

- Files resolved.
- Important choices, especially where one side's change was dropped.
- Build, lint, and test results.
- The command the user should run next (for example `git commit` or `git rebase --continue`).
