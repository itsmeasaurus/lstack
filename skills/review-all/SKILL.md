---
name: review-all
description: Run the bugs/security review and the code-quality review in parallel, then merge them into one report. Use for "full review", "review everything", or "both reviews". Local and read-only.
argument-hint: "[base branch or PR number, optional]"
disable-model-invocation: true
---

# Full review

Run two reviews of the current branch at the same time, then combine them. Do not edit files. **Never** push, commit, comment, or post anywhere.

1. Work out the base branch: $ARGUMENTS if given, otherwise the PR base or the repo's default branch.
2. In one message, start two general-purpose subagents so they run in parallel:
   - Subagent A: "Read `${CLAUDE_SKILL_DIR}/../review-bugs/SKILL.md` and follow it exactly for base `<base>`. Return its report."
   - Subagent B: "Read `${CLAUDE_SKILL_DIR}/../review-quality/SKILL.md` and follow it exactly for base `<base>`. Return its report."
3. When both finish, write one report:
   - A one-line overall verdict.
   - All findings, highest risk first, with duplicates merged. A problem both reviewers found counts as stronger evidence.
   - Where they disagree, check the code and decide. Say what you decided.
   - Anything still unverified.

Keep it short. Don't paste both reports in full.
