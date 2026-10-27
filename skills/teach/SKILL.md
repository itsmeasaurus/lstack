---
name: teach
description: Teach a part of the codebase so the user really understands it, by combining the how and why skills into one plain explanation. Use for "teach me X", "help me really understand X", "explain this change or subsystem to me".
argument-hint: "[what to learn]"
---

# Teach

Help the user understand $ARGUMENTS: what it is, how it works, and why it is built that way. The goal is understanding. Do not change any code.

## Steps

1. From the conversation, work out why they are asking (about to change it, reviewing it, debugging it, new to it) and what they already know. Pick the 2 or 3 things they most need to understand. Skip what they already know.
2. Read enough code to get oriented. Then run the **how** skill for how it works and the **why** skill for why. For a small target, one of them may be enough. Keep the why question narrow unless the reasons are the main point.
3. Combine the results into one explanation. Reword freely, but keep why's confidence labels (Confirmed / Likely / Guess) exactly as they are.

## How to explain

- Start with a plain definition. Name the thing in general terms, with its common name if it has one (for example "this is a debounce"). Then link it to this code: "here, we use it to ...".
- For each part, say what problem it solves and how it works. A list of functions is a reference, not teaching.
- Give the smallest complete answer first: one to three sentences. Then stop and offer to go deeper. Add layers only when asked.
- For anything with 3 or more moving parts, use a short series of mermaid diagrams. Each one redraws the last and adds one part, so the user sees the system build up. Don't start with one big diagram of everything.
- Show real code or a diff when it is the fastest way to make the point.

## Style

- Plain spoken English, like explaining to a colleague.
- Short sentences. One name per concept, used the same way every time.
- No filler labels such as "key insight", "TL;DR", "at its core", or "this is the tricky part". Just say it.
- No quizzes and no lecturing.
- Reply with the explanation itself, not a report of what you did.
