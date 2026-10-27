---
name: ketchup
description: Catch the user up on what happened in this chat since their last message, in plain words, and list every decision waiting on them. Use for /ketchup or "catch me up".
disable-model-invocation: true
---

# Ketchup

Catch the user up on what changed since the last message **they** wrote before `/ketchup`. Tool results, notifications, and subagent reports are not their messages.

Read-only: don't change code, start jobs, or post anything. Re-check the current state of anything you report (a test run, a file, a branch) instead of trusting earlier output.

## Write it like this

Use plain words and short sentences, like one person catching up another. Say what changed for the user, not how you did it ("the tests pass", not "exit code 0"). Leave out hashes, file paths, and commands unless they need one to act.

1. **First sentence**: what's waiting on the user, or "Nothing needs you."
2. **What happened**: one short line per thing they asked for: what came of it, and whether it's done, still running, failed, or not checked. Under about 100 words total. Skip work that changed nothing for them. Add a small mermaid diagram only when a picture really helps (how parts connect, before vs. after). Max six boxes.
3. **Waiting on you**: each decision only the user can make (a product choice, an approval, something irreversible, access you lack). For each:
   - The decision, and your recommendation.
   - What it changes for users, and the evidence behind your pick.
   - The risk, or for a choice between options, what each option gains and costs.
   - Write "unknown" for any needed fact you don't have.

Never invent a decision to fill the list. Work you can still do yourself is not a decision for the user.
