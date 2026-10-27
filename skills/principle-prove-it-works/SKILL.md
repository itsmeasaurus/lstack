---
name: principle-prove-it-works
description: Apply after finishing a task, before saying it's done. Check the real result directly (run it, read the actual value, inspect the diff), not a proxy or "it compiles".
user-invocable: false
---

# Prove it works

Before saying something is done, check the real thing.

- Run the feature, call the endpoint, read the actual value. "It compiles" and "the code looks right" are not proof.
- Check exit codes and full output. A truncated output (`| tail -1`) or your own `echo` proves nothing.
- Before reporting success (started, sent, saved, merged), read the real state.
- If a check fails, first suspect the way you checked, then the system.
- A red test is only proof if it fails with the mismatch you predicted. A crash or an empty result also shows red. Quote the actual failure.
- Check the process too: for each fact you relied on, know where it came from (the real file, the real config), not from memory or a guess.
- When you can, write a small script that repeats the check, run it, and show the output, so the user can re-run it instead of trusting you.

When reporting, say clearly what you verified and how, and what you did not verify.
