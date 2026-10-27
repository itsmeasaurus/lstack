---
name: sharpen
description: Sharpen a task before starting by working out how an expert would approach it, what the user really wants, and whether the request is over- or under-specified. Use for /sharpen.
disable-model-invocation: true
---

Before starting the task, think it through and briefly report:

1. **Expert approach**: how a top expert would do this. Their real sources, their real methods, and how they would check the result is right.
2. **Real goal**: what the user is actually trying to achieve, beyond the literal request.
3. **Specification**: is the task too tight or too loose? Point out constraints that don't serve the goal and could be dropped, as well as missing ones that should be added.
4. **Open choices**: decisions that belong to the user. List them; don't decide them silently.

Keep it short. Then ask whether to proceed with the sharpened version.
