---
name: blast-radius
description: Find what a change could break outside the diff, and prove the main safety assumption by running real code. Use for "blast radius of X", "what could this break", or checking a small diff you don't trust.
argument-hint: "[change, file, or PR to check]"
---

# Blast radius

Find what $ARGUMENTS could break somewhere else, beyond the diff. Listing callers is not the job; anyone can grep that. The job is the breakage grep won't show.

**Never** push, commit, comment, or post anywhere. You may write small local test scripts, but tell the user where they are and don't commit them.

## Steps

1. **Read the change**: what it adds, changes, and deletes, and what it now does differently, including the parts the diff doesn't spell out.
2. **Find the one fact it's safe because of.** Most risky-looking changes are safe because of a single fact (for example "this only removes cache entries that are already expired"). Find it. Spend your effort here, not on a long list of maybes.
3. **Look where grep stops**: library source code at the pinned version in `package.json` / lockfile; timing (promises, event loop, startup and shutdown order); things a symbol search misses, such as JSON returned by an API, DB columns, message formats, env variables, feature flags, and code several steps downstream.
4. **Rate each risk honestly**: how likely, and how bad. Cite a real `file:line`. Never invent a caller or an API. "I searched and found nothing" is a valid result.
5. **Prove the one fact.** Write a small script or test that calls the real code and fails loudly if you're wrong. Run it and show the output. If you can't, mark the fact *unproven*.

## How sure are you

Say how far you got for the key fact:
1. Stated only (worthless alone) → 2. Pointed at the line → 3. Walked the failure case and showed it can't happen → 4. Ran code that proves it → 5. Reproduced it in the running app.

## Report

- **What it does**: including the non-obvious part.
- **The one fact it's safe because of**: the fact, how sure (1–5), and the proof, or *unproven*.
- **Risks**: how it breaks, `file:line`, likelihood and cost, how to check.
- **Cleared**: what you checked and why it's fine.
- **Before you merge**: the cheapest test that would catch the real problem, including the script you wrote.
