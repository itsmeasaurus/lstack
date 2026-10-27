---
name: what-did-i-get-done
description: Summarize my own commits over a time period into a short status update. Use for "what did I get done", standup notes, or weekly updates.
argument-hint: "[time period, e.g. yesterday, last week]"
disable-model-invocation: true
allowed-tools: Bash(git log *) Bash(git config user.email) Bash(git show *)
---

# What did I get done

Summarize my work for: $ARGUMENTS (default: yesterday).

1. Turn the period into real dates (today's date is the reference).
2. Get my email with `git config user.email`.
3. List my commits: `git log --all --no-merges --author="<email>" --since="<start>" --until="<end>"`. Use `git show --stat` on a commit if its message is unclear.
4. Ignore uncommitted work and merge commits.

## Write the update

- One short summary suitable for a standup or status message.
- The real date range used.
- Optionally 2 to 5 bullets for the biggest changes only.

Rules: very concise. Focus on real behavior or architecture changes. Skip formatting, import cleanup, and small renames. Describe what changed; don't guess at why.
