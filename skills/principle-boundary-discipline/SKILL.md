---
name: principle-boundary-discipline
description: Apply when adding validation, error handling, or framework glue code. Validate at system edges (HTTP, CLI, config, env, external APIs, queues), trust types inside, and keep business logic in pure functions.
user-invocable: false
---

# Boundary discipline

Validate and handle errors where data **enters** the system. Inside, trust the types.

**At the edges** (HTTP requests, CLI arguments, env variables, config files, external API responses, queue messages, DB reads of untrusted data):
- Validate and parse into a named domain type, once.
- Return clear errors. Be defensive here.

**Inside the system**:
- Use the typed data. Don't re-check it deep in the call chain.
- Let errors propagate instead of catching and re-wrapping at every level.

**Across the edge**:
- Expose domain types, not the edge's raw shapes. Don't pass framework request objects, ORM models, or raw API payloads deep into business logic, and don't re-export them from your public API.

**Code layout**:
- Business logic lives in pure functions with no framework dependencies, so it's easy to test.
- Route handlers, controllers, and consumers stay thin: parse input, call the logic, format the output.

Two quick tests:
- "Is this data crossing an edge right now?" If not, this validation is probably redundant.
- "Could this be a pure function the handler just calls?" If yes, extract it.
