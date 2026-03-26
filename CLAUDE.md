# Devil's Advocate

Claude Code skill for deep research verification and claim triage.

## Structure

```
skills/
  devilsadvocate/SKILL.md    # Standalone skill (full claim triage)
  _perspectives/
    skeptic.md                # Automatic perspective (lightweight, always-on)
    README.md                 # Perspective system documentation
```

## Conventions

- Skill files use YAML frontmatter with `name`, `description`, and optional model/trigger fields
- The standalone skill runs in main conversation context
- The skeptic perspective runs as a background subagent (haiku by default, escalates to sonnet)
- Output formats are strict — orchestrators parse them programmatically
