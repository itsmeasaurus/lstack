---
name: principle-smallest-change
description: Apply when refactoring, judging diff size, or tempted to add abstractions, layers, or options. Prefer deleting code and the smallest change that solves the problem.
user-invocable: false
---

# Smallest change

- **Smallest diff that solves the problem.** Fewer lines beat "elegant" boilerplate.
- **Delete before adding.** Remove dead code, unused options, and duplicate checks first, then build on the simpler base.
- **One decision, one place.** Don't repeat the same choice in several files. Put it behind one source of truth and pass the result down.
- **No speculative abstraction.** Don't add a layer, interface, config option, or parameter "for later". Add it when a second real use appears.
- **No pass-through wrappers.** A function that only calls another function adds a layer to read and nothing else.
- **Don't keep old and new side by side** longer than needed. When replacing an internal API, move all callers and delete the old one in the same change.
