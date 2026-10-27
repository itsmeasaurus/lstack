# lstack

My personal Claude Code skills, distributed as a plugin marketplace.

## Install

```
/plugin marketplace add itsmeasaurus/lstack
/plugin install lstack@lstack
```

Or from your terminal:

```
claude plugin marketplace add itsmeasaurus/lstack
claude plugin install lstack@lstack
```

Restart Claude Code after installing so the skills load.

## Update

```
/plugin marketplace update lstack
```

## Skills

Plugin skills are namespaced, so you call them as `/lstack:<skill>`, for example
`/lstack:review-bugs main`. Most of them also load on their own when you ask a
matching question ("why is this check here?", "CI is failing").

### Understand code

| Skill | What it does |
|---|---|
| `how` | Explains how a module, feature, or flow works. Uses parallel Explore subagents for big areas. |
| `why` | Finds out why code is built the way it is, from git history and PRs. Labels each reason Confirmed / Likely / Guess. |
| `teach` | Combines `how` and `why` into one plain explanation, built up step by step. |
| `bro` | Restates Claude's last message in plain, simple words. Manual only (`/lstack:bro`). |

### Review and ship

| Skill | What it does |
|---|---|
| `review-bugs` | Deep review of your branch for bugs, broken callers, security holes, dev-setup breakage, and feature-flag leaks. |
| `review-quality` | Strict maintainability review: structure, needless layers, file size, weak types, and simpler rewrites. |
| `review-all` | Runs `review-bugs` and `review-quality` in parallel and merges them into one report. Manual only (`/lstack:review-all`). |
| `blast-radius` | Finds what a change could break outside the diff, and proves its main safety assumption by running real code. |
| `ci-fix` | Finds why the PR's CI is red and fixes it in your working tree. |
| `pr-comments` | Turns review comments on your PR into a prioritized to-do list. |
| `pr-prep` | Drafts a PR description and reviewer notes, and suggests how to regroup or split commits. |

## Good to know

- **Nothing gets pushed or posted.** Every skill is local. None of them commit,
  push, comment on, approve, or edit a PR. `ci-fix` edits files in your working
  tree and leaves the commit to you. `blast-radius` may write small throwaway
  test scripts and tells you where they are.
- **You need `git`, and the GitHub CLI (`gh`) signed in** (`gh auth login`) for
  `ci-fix`, `pr-comments`, `pr-prep`, `review-*`, and `why`. Without `gh` they
  still work on the local diff and history, but can't read PRs or CI logs.
- **GitHub only.** PR and CI steps use `gh`. On GitLab, Azure DevOps, or
  Bitbucket, the PR parts won't work as written; swap the `gh` commands for
  your platform's CLI.
- **Some commands will ask for permission.** Each skill's `allowed-tools` only
  pre-approves read-only commands. Running your tests or build (`ci-fix`,
  `blast-radius`), editing files (`ci-fix`), and the `gh api` call in
  `pr-comments` go through your normal permission prompts on purpose.
- **Some skills depend on others.** `review-all` reads `review-bugs` and
  `review-quality` from sibling folders, and `teach` uses `how` and `why`. If
  you copy one of them, copy the ones it uses too.
- **Any language works.** Some wording leans JavaScript/Node (`package.json`,
  lockfiles, promises), but the steps apply to any stack.
- **Base branch.** The review skills take an optional base branch or PR number.
  Without one they use the PR's base, then the repo's default branch.

## Credits

These skills are inspired by [pstack](https://github.com/cursor/plugins/tree/main/pstack)
by Lauren Tan, originally a skill stack for Cursor (MIT License). `how`, `why`,
`teach`, `bro`, and `blast-radius` are adapted from pstack skills of the same name.
For Claude Code, see also the [pstack-claude](https://github.com/michael-denyer/pstack-claude)
port by Michael Denyer.

## Use them as your own

Feel free to copy any skill in `skills/` into your own setup (for example
`~/.claude/skills/<skill-name>/`) and change it however you like. Copied there,
they are no longer namespaced: `/review-bugs` instead of `/lstack:review-bugs`.
Everything here is under the [MIT License](LICENSE).

## Adding a skill

Create `skills/<skill-name>/SKILL.md` with frontmatter:

```markdown
---
name: skill-name
description: What it does and when Claude should use it.
---

Instructions...
```

Bump `version` in `.claude-plugin/plugin.json` so installs pick up the change.
