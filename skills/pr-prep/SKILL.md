---
name: pr-prep
description: Make a pull request easier to review, by drafting a clear PR description and reviewer notes, and suggesting how to split or regroup commits. Use for "make this easy to review", "write the PR description", or "tidy this PR". Never pushes or posts.
argument-hint: "[PR number or base branch, optional]"
allowed-tools: Read Grep Glob Bash(gh pr view *) Bash(git diff *) Bash(git log *) Bash(git show *) Bash(git status *)
---

# PR prep

Help a reviewer understand the change fast. Do not change code behavior. **Never** push, force-push, edit the PR, comment, or post anything. Give the user text to paste themselves.

1. Find the target: $ARGUMENTS, the current branch's PR, or the default branch as base.
2. Read the commits, diff size, changed paths, generated files, and the current PR description.
3. Spot what makes it hard to review: noisy commits, a description that no longer matches the diff, unrelated changes, mechanical and logic changes mixed together, missing tests, no clear starting point.

## Output

**PR description draft** (in a code block, ready to paste):
- A short summary that matches the actual diff.
- Core files to review first, separate from generated or mechanical files.
- Risky behavior changes, migration or rollout order, and test coverage.

**Commit plan** (suggestion only): a better grouping, usually in this order: schema/storage → core logic → wiring → UI → tests.
Only rewrite local history if the user asks. If they do: record `git rev-parse HEAD^{tree}` first, compare it after, and stop if the tree changed. Never push.

**Split advice**: if the PR is too big to fix with notes, say so and suggest how to split it.

Never hide a real behavior change inside "cleanup".
