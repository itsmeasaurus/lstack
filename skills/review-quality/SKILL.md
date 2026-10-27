---
name: review-quality
description: Strict maintainability review of the current branch's changes, looking for messy structure, needless abstractions, giant files, scattered if-statements, and weak types, plus simpler ways to write the change. Use for "code quality review", "is this clean", or "how can this be simpler". Local and read-only.
argument-hint: "[base branch or PR number, optional]"
allowed-tools: Read Grep Glob Bash(git diff *) Bash(git log *) Bash(git show *) Bash(git merge-base *) Bash(gh pr view *) Bash(wc *)
---

# Review: code quality

Review how the current branch's changes are built, not whether they work. Report and suggest. Do not edit files.

**Never** push, commit, comment, approve, or post anywhere.

## 1. Get the diff

- Base: use $ARGUMENTS if given. Otherwise use the PR base from `gh pr view --json baseRefName`, or the repo's default branch.
- Diff: `git diff <base>...HEAD`. Read the surrounding code too, not just the changed lines.

## 2. Be ambitious

Don't stop at small cleanups. Look for a restructure that keeps the behavior but makes the change much smaller and simpler: whole branches, helpers, modes, or layers that could disappear. Prefer deleting complexity over moving it around.

## 3. Rules to apply

1. **File size**: flag any file this branch pushes from under 1,000 lines to over 1,000. Suggest how to split it.
2. **Scattered conditions**: flag new one-off `if` statements and special cases added to unrelated flows. Suggest a proper home: a helper, a policy object, a state machine, or a separate module.
3. **Working is not enough**: if the same behavior could have a clearly cleaner structure, say so.
4. **Boring over clever**: flag "magic" code, thin wrappers, and pass-through helpers that add a layer without adding clarity.
5. **Types and boundaries**: flag `any`, `unknown`, many casts, needless optional fields, and loose object shapes where a clear type would work. Flag silent fallbacks that hide an unclear rule.
6. **Right layer**: flag feature logic leaking into shared code, and new one-off helpers when an existing one already does the job.
7. **Flow**: flag independent work run one after another for no reason, and related updates that can leave data half-updated.

## 4. Report

Start with a one-line verdict. Then list findings, most important first:

- **[High / Medium / Low] Title** — `file:line`
  - The problem, in one or two sentences.
  - The simpler version: describe it, with a short code sketch if it helps.

Skip pure style nits that a linter or formatter would catch.
