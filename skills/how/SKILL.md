---
name: how
description: Explain how a part of this codebase works (a module, feature, flow, or subsystem). Use for "how does X work", walkthroughs before changing code, and "where does this live / which layer owns this" questions. For the reasons behind a design, use the why skill.
argument-hint: "[what to explain]"
allowed-tools: Read Grep Glob
---

# How

Explain how $ARGUMENTS works, so a senior engineer new to this area can build a working mental model. Read only. Never edit files.

## 1. Size the question

- **Small** (one function, one file, one narrow question): read the code yourself and answer.
- **Large** (spans several files, packages, or services): split it into 2 to 4 angles, for example entry points, data flow, storage, error handling. Start one Explore subagent per angle, all in one message so they run in parallel. Ask each to return file paths, key symbols, and the flow it found. Then combine their findings and check any conflict against the code yourself.

If the target is unclear, state your best guess in one line and continue. The user can redirect.

## 2. Write the explanation

Use these sections. Drop any that add nothing.

- **Overview**: 1 to 2 short paragraphs. What it is, what it does, why it exists.
- **Key concepts**: the few types, services, or ideas needed to follow the rest. One line each.
- **How it works**: the main part. What triggers it, what happens step by step, where data goes, where decisions are made. Name real files and functions. Prose, not pseudocode. Add a mermaid diagram only when 3 or more parts talk to each other.
- **Where things live**: the handful of files someone needs to start working here.
- **Gotchas**: surprising behavior and traps. Skip if there are none.

## Style

- Concrete: "`OrderService.create()` calls `stripe.charge()`", not "the service delegates to the client".
- Explain why something complex is complex. Don't pad simple things.
- Say plainly what you could not confirm from the code.
