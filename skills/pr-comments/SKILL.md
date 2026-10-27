---
name: pr-comments
description: Fetch the review comments on the current branch's pull request and turn them into a short, prioritized to-do list. Use for "what did reviewers say", "summarize PR feedback", or "PR comments". Read-only.
argument-hint: "[PR number, optional]"
allowed-tools: Bash(gh pr view *) Bash(gh repo view *)
---

# PR comments

Summarize the feedback on a pull request. Read only. **Never** reply, resolve, approve, comment, or post anything.

1. Find the PR: $ARGUMENTS if given, otherwise the PR for the current branch (`gh pr view --json number,url,title`).
2. Get the discussion and reviews: `gh pr view <n> --comments` and `gh pr view <n> --json reviews`.
3. Get inline code comments with a **read-only** call: `gh api repos/{owner}/{repo}/pulls/<n>/comments`. Do not add `-X`, `--method`, `-f`, `-F`, `--field`, `--raw-field`, or `--input`; those can make it a write call.
4. Group the feedback:
   - **Must fix**: bugs, blockers, requested changes.
   - **Should consider**: design or quality suggestions.
   - **Questions**: things a reviewer asked that need an answer.
   - **Already handled / outdated**: comments on code that has since changed.

Report a prioritized action list. For each item: who said it, `file:line` if any, and what to do in one line.
