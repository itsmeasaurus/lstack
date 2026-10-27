---
name: why
description: Find out why code is built the way it is, using git history and pull requests. Use for "why does X work this way", "why did we pick Y", "why is this check here", regressions, and design tradeoffs. For how code works at runtime, use the how skill.
argument-hint: "[code, file, or decision to investigate]"
allowed-tools: Read Grep Glob Bash(git log *) Bash(git blame *) Bash(git show *) Bash(gh pr view *)
---

# Why

Investigate why $ARGUMENTS is the way it is. Be a careful investigator: keep what you found separate from what you guess. Read only. Never edit files, push, comment, or post anywhere.

## Sources

Use only local and source-control evidence:

1. The code itself: comments, TODOs, tests, naming.
2. Git history: `git blame -L <start>,<end> <file>`, `git log --follow -p -- <file>`, `git log --oneline -20 -- <file>`, `git show <commit>`.
3. Pull requests: find PR numbers in commit subjects like `(#1234)`, then `gh pr view <number> --comments`.
4. Ticket IDs mentioned in commits or PRs (for example `ABC-123`): report them so the user can look them up. Do not fetch them.

Do not query chat, docs, issue trackers, or any other external service unless the user asks.

## Steps

1. Pin the target: file paths, line ranges, key symbols. If unclear, state your best guess in one line and continue.
2. Trace history back to the commit that introduced the behavior, not just the last one that touched it. Follow renames.
3. Read the PR description and review comments for the commits that matter.
4. If the code looks defensive (retries, null checks, timeouts, feature flags), look for the bug or incident that caused it in later commits and PRs.

## Answer

Lead with the answer in 1 to 3 sentences. Then:

- **Evidence**: each reason, with its source (commit hash, PR number, file:line).
- **Confidence**: mark each reason as
  - *Confirmed*: a commit, PR, or comment says so directly.
  - *Likely*: strong indirect evidence. Say what it is.
  - *Guess*: inferred from the code alone. Say so.
- **Gaps**: what you searched and found nothing, and where the answer might live instead (for example a ticket ID).

Never present a guess as a fact.
