# Contributing

Contributions welcome. This is a Claude Code skill — the primary artifacts are markdown files with specific structure.

## Guidelines

1. **Preserve the output format** — downstream tools parse the Objective Alignment Brief structure programmatically. Changes to section headers or symbol conventions (`[V]`, `[P]`, `[U]`, `[X]`) are breaking changes.

2. **Keep it focused** — this skill does one thing: verify research claims. It doesn't implement, it doesn't research, it doesn't plan. Scope creep is the enemy.

3. **Test with real research output** — run `/devilsadvocate` on actual AI-generated research and verify the triage catches real hallucination patterns. Synthetic tests miss the subtle failure modes.

4. **Hallucination taxonomy is extensible** — if you encounter a new failure mode not covered by the 5-type taxonomy (intrinsic, extrinsic, entity, attribution, citation), propose it with examples.

5. **Simplicity filter is the soul** — the skill's bias toward simplicity is intentional and non-negotiable. Complexity must earn its place.

## Structure

- `skills/devilsadvocate/SKILL.md` — the standalone skill (invoked manually)
- `skills/_perspectives/skeptic.md` — the automatic perspective (fires on every pipeline step)
- Changes to the skeptic should maintain the input contract and output format sections

## Pull Requests

- One logical change per PR
- Include before/after examples if changing triage logic
- Update README.md if adding new features or changing usage
