---
name: principle-test-behavior
description: Apply when writing, changing, or keeping a test. Test what the code's users can observe, so the test fails when behavior breaks and still passes when only the internals change.
user-invocable: false
---

# Test behavior, not implementation

A test is a promise about what the code does for its users: a caller, an end user, or another service. Behavior is what they can observe: return values, errors, data they can read back, and effects outside the code (a request sent, a row written, a message published).

Judge each test with two imagined edits:

1. **Break the behavior** (wrong value, skipped effect, effect done twice). If the test still passes, it proves nothing. Common causes: a loose assertion, an expected value computed by the code under test, or only checking that a mock was called.
2. **Change the internals** but keep every observable result the same. If the test now fails, it's tied to the implementation and will break on every refactor without catching bugs.

Keep tests that catch edit 1 and survive edit 2. Rewrite or delete the rest.

To write a good test:
- Call the code through the same interface its users use, with a concrete input.
- Take the expected value from the requirement, not from running the code.
- Mock only external systems you can't run locally. When you assert a mock was **not** called, pair it with a case where it **is** called, to prove the test can see the call.
- A test can also pin a rule (an invariant) or a documented default; name the promise it protects.
