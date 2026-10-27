---
name: principle-fix-root-causes
description: Apply when debugging. Trace each symptom back to the first place things went wrong and fix it there, not where the error showed up.
user-invocable: false
---

# Fix root causes

The **symptom** is where a bad state became visible. The **root cause** is the first place the code did something wrong, or failed to handle a state it should handle. Fix the root cause. A symptom fix hides the evidence and lets the bug appear somewhere else.

- Reproduce the bug first.
- Keep asking "why?" until the answer is a wrong decision in the code, not a result of an earlier one.
- When stuck, add logging or a debugger. Read the actual error and the actual values. Don't guess.
- Ask whether the bad state is **legitimate**:
  - If the system may really be in that state, the code that broke on it is the root cause. Handle the state there.
  - If the state should never exist, a check where it broke just hides the bug. Find what created the state.
- If it only fails after a restart, suspect saved state first: config, cache, lock files, stored sessions.
- Fix the pattern, not just the instance. Find every place with the same mistake.
- If a workaround needs a long comment to justify it, the code is wrong.
- If the key fact was hard to find, suggest a cheap, always-on signal (a log line, a metric, a clear error) that would have shown it immediately.
