---
name: review-bugs
description: Deep review of the current branch's changes for bugs, broken existing features, security holes, broken local dev setup, and feature-flag leaks. Use for "review my branch", "find bugs in this diff", "security review", or "deep review". Local and read-only.
argument-hint: "[base branch or PR number, optional]"
allowed-tools: Read Grep Glob Bash(git diff *) Bash(git log *) Bash(git show *) Bash(git merge-base *) Bash(git status *) Bash(gh pr view *)
---

# Review: bugs and security

Review the current branch's changes. Report problems only. Do not edit files.

**Never** push, commit, comment, approve, or post anywhere. Never run `git push`, `gh pr comment`, `gh pr review`, `gh pr edit`, or a `gh api` write call.

## 1. Get the diff

- Base: use $ARGUMENTS if given. Otherwise use the PR base from `gh pr view --json baseRefName`, or the repo's default branch.
- Diff: `git diff <base>...HEAD`. Also read `git log <base>..HEAD` to learn what the branch is trying to do.

## 2. What to look for

Only report problems in code that this branch **adds or changes**. Ignore old problems in untouched code.

- **Bugs**: wrong logic, missing error handling, null/undefined cases, race conditions, off-by-one, wrong async/await use.
- **Broken existing features**: trace each change to its callers and users, across modules and packages. Small changes often break something far away.
- **Security**: injection, missing auth or permission checks, secrets in code or logs, unsafe input handling, data exposed to the wrong users.
- **Broken dev setup**: changed env variable names, new required env variables, changed secret locations, port changes, new manual setup steps.
- **Feature-flag leaks**: code meant to stay behind a flag or internal check that is now reachable without it.

## 3. Rules

- Finish your research before reporting. If you can check something in the code, check it. Don't write "this is fine if the backend handles it" when you can read the backend.
- Don't over-report. A wrong "High" makes people stop trusting the review.
- If the branch clearly *means* to remove a safeguard or feature and the change is contained, don't report it, unless the author likely missed a serious side effect.
- After your own review, if a PR exists, read its comments with `gh pr view <n> --comments`. Check any issues others found that you missed, and mark which findings came from them.

## 4. Report

Start with a one-line verdict. Then list findings, highest risk first:

- **[High / Medium / Low] Title** — `file:line`
  - What goes wrong and when.
  - Evidence: the code path you traced.
  - Suggested fix (describe it, don't apply it).

End with anything you could not verify. If you found nothing important, say so plainly.
