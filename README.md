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

## Get new skills

New skills and changes land whenever this repo gets a new commit. Claude Code
doesn't pull them for you unless you turn on auto-update, which is off by default
for marketplaces outside Anthropic's own.

- **Turn on auto-update (once):** run `/plugin`, open the **Marketplaces** tab,
  select `lstack`, and choose **Enable auto-update**. Claude Code then checks
  for updates shortly after each session starts.
- **Or update by hand:** run `claude plugin update lstack@lstack` in your
  terminal.

Either way, the new version loads in your next session, or after
`/reload-plugins` in the current one.

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

### Plan and talk

All manual only: call them by name.

| Skill | What it does |
|---|---|
| `bro` | Restates Claude's last message in plain, simple words. |
| `sharpen` | Before starting, works out how an expert would approach the task, your real goal, and the choices that are yours. |
| `in-your-own-words` | Restates your goal and problem, then waits for you to confirm before starting. |
| `ketchup` | Catches you up on what happened since your last message, and lists every decision waiting on you. |
| `what-did-i-get-done` | Turns your own commits over a period into a standup or status update, for example `/lstack:what-did-i-get-done last week`. |

### Write code

| Skill | What it does |
|---|---|
| `architect` | Sketches two or more designs as types and signatures, picks one with you, then builds against it. |
| `tdd` | Fixes a bug by first writing a test that fails because of it. |
| `deslop` | Removes AI-style clutter from your branch: needless comments, over-defensive checks, `as any`, deep nesting. |
| `no-comments` | Deletes comments that add nothing, and flags code that needed one because it's unclear. |
| `fix-merge-conflicts` | Resolves merge or rebase conflicts, runs build, lint, and tests, and stages the result for you to commit. |

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

### Background principles

You don't call these. Claude loads them by itself when the work fits, and they
don't appear in the `/` menu.

| Skill | When it applies |
|---|---|
| `principle-boundary-discipline` | Adding validation or error handling: check at the edges, trust types inside. |
| `principle-fix-root-causes` | Debugging: fix the first thing that went wrong, not where the error showed up. |
| `principle-prove-it-works` | Before saying a task is done: check the real result, not "it compiles". |
| `principle-smallest-change` | Refactoring or adding layers: prefer deleting code and the smallest diff. |
| `principle-test-behavior` | Writing or keeping tests: test what users can observe, not the internals. |
| `typescript-best-practices` | Reading or editing `.ts` and `.tsx` files. |

## Good to know

- **Nothing gets pushed or posted.** Every skill is local. None of them commit,
  push, comment on, approve, or edit a PR. `ci-fix` edits files in your working
  tree and leaves the commit to you. `blast-radius` may write small throwaway
  test scripts and tells you where they are. `tdd`, `deslop`, `no-comments`,
  `architect`, and `fix-merge-conflicts` change files but never commit;
  `fix-merge-conflicts` stages the result and leaves `git commit` or
  `git rebase --continue` to you.
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
  `review-quality` from sibling folders. `teach`, `architect`, and
  `no-comments` use `how` and `why`. If you copy one of them, copy the ones it
  uses too.
- **`what-did-i-get-done` finds your commits by `git config user.email`.**
  Commits you made with another email (another machine, or GitHub's web
  editor) won't show up.
- **Any language works.** Some wording leans JavaScript/Node (`package.json`,
  lockfiles, promises), but the steps apply to any stack.
- **Base branch.** The review skills take an optional base branch or PR number.
  Without one they use the PR's base, then the repo's default branch.

## Credits

These skills are inspired by [pstack](https://github.com/cursor/plugins/tree/main/pstack)
by Lauren Tan, originally a skill stack for Cursor (MIT License). Most skills
here are adapted from pstack skills of the same or a similar name: `how`, `why`,
`teach`, `bro`, `blast-radius`, `architect`, `sharpen`, `in-your-own-words`,
`ketchup`, `tdd`, `no-comments`, `typescript-best-practices`, `deslop` (from
`unslop`), and the `principle-*` skills.
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

Commit and push. `plugin.json` has no `version` on purpose: Claude Code uses the
commit SHA instead, so every push counts as a new version. If you ever add a
`version`, you must bump it on every release, or users won't get updates.
