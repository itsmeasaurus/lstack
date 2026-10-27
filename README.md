# lstack

My personal Claude Code skills, distributed as a plugin marketplace.

## Install

```
/plugin marketplace add itsmeasaurus/lstack
/plugin install lstack@lstack
```

## Update

```
/plugin marketplace update lstack
```

## Adding a skill

Create `skills/<skill-name>/SKILL.md` with frontmatter:

```markdown
---
name: skill-name
description: What it does and when Claude should use it.
---

Instructions...
```

Bump `version` in `.claude-plugin/plugin.json` so installs pick up the change.

## Use them as your own

Feel free to copy any skill in `skills/` into your own setup (for example
`~/.claude/skills/<skill-name>/`) and change it however you like. Everything
here is under the [MIT License](LICENSE).
