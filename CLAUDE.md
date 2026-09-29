# Devil's Advocate

Claude Code skill for deep research verification and claim triage.

## Where to go

This repo follows ICM (Jake Van Clief's folder method): this file routes, each room's
`CONTEXT.md` holds its contract.

| Task                                                                 | Go to                    | Read                                                                 | Skills |
| -------------------------------------------------------------------- | ------------------------ | -------------------------------------------------------------------- | ------ |
| Change the standalone full-depth claim-triage skill                  | `skills/devilsadvocate/` | [skills/devilsadvocate/CONTEXT.md](skills/devilsadvocate/CONTEXT.md) | none   |
| Change the automatic skeptic perspective (fires every pipeline step) | `skills/_perspectives/`  | [skills/_perspectives/CONTEXT.md](skills/_perspectives/CONTEXT.md)   | none   |

Root files stay where their tools expect them: `README.md` (GitHub landing page, install
instructions), `CONTRIBUTING.md`, `LICENSE`.

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
