---
name: no-comments
description: Remove code comments that add nothing (narration, banners, commented-out code, workaround excuses) from the current changes, and flag code that needed a comment because it's unclear. Use for "remove useless comments" or /no-comments.
argument-hint: "[files or base branch, optional]"
---

# No comments

Scope: $ARGUMENTS if given, otherwise the current branch's diff against the default branch, plus uncommitted changes. Only touch comments in that scope. Never commit, push, or post anywhere.

## Delete

- Narration that restates the code (`// loop over users`).
- Section banners and decorative separators.
- Commented-out code.
- Long excuses for workarounds. If code needs a paragraph to justify it, the code is the problem: delete the comment and flag the code (see below).

## Keep

- License or legal headers.
- Comments explaining behavior forced by something you **can't change**: a third-party library, a platform, a vendor API, a protocol. Surprises in your own code don't count.
- Doc comments (JSDoc/TSDoc) that define a public API.
- Links to issues or RFCs that explain a constraint the code can't express.
- `// prettier-ignore`.

When unsure, read the nearby code (or run the **how** / **why** skill) before deciding.

## Lint and type suppressions

For `eslint-disable`, `@ts-ignore`, `@ts-expect-error`: look up the rule. If it's a style-only or noisy rule, keep the suppression. If the rule protects correctness or safety, flag the code that triggered it. Don't remove the suppression unless you also fix the code.

## Constraint comments

For comments like "do not remove", "don't change this wording", or "ask X before changing": suggest a cheaper enforcement (a type, a test, a runtime check, a lint rule) and **ask before** adding it. Don't delete these without the user's OK.

## Flag, don't fix

When a deleted comment was explaining unclear code in our own codebase, don't rewrite the code. Flag it: the symbol, `file:line`, and the fix it needs (rename, extract, better type, or redesign).

## Report

Files changed, number of comments removed, comments kept and why, flagged code, and constraint comments waiting on the user.
