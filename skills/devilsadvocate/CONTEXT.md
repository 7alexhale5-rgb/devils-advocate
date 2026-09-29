# Devilsadvocate room: the standalone full-depth claim-triage skill

One job: keep the manually-invoked `/devilsadvocate` skill accurate to its documented output
contract. Paths are relative to the repo root.

## Inputs

- The skill definition: `skills/devilsadvocate/SKILL.md` (YAML frontmatter — `name`,
  `description`, trigger phrases — plus the step-by-step triage procedure).
- The documented contract: `README.md` § Claim Triage System, § Output Format, § Principles —
  the `[V]/[P]/[U]/[X]` symbols and the Objective Alignment Brief section headers are a
  breaking-change surface (`CONTRIBUTING.md` point 1).
- Missing input: a change that alters a section header or symbol without updating both
  `README.md` and `CONTRIBUTING.md` point 1 is incomplete — do not ship it half-updated.

## Process

1. Edit `skills/devilsadvocate/SKILL.md` — frontmatter (`name`, `description`, trigger
   phrases) or the numbered triage steps.
2. If the change touches the Objective Alignment Brief's structure (section headers, the
   `[V]/[P]/[U]/[X]` symbols, or the hallucination taxonomy's five types), update
   `README.md` § Output Format and § Claim Triage System to match, in the same change.
3. NOT FOUND: no automated test or lint command exists in this repo (no `package.json`,
   `Makefile`, or `pyproject.toml`) — verification is manual, per Human check below.

## Outputs

- Changed `skills/devilsadvocate/SKILL.md`.
- Matching edits to `README.md` when the output contract changed.

## Human check

Alex (or a contributor) runs `/devilsadvocate` on real AI-generated research output —
`CONTRIBUTING.md` point 3: "Synthetic tests miss the subtle failure modes." Pass: the triage
catches real hallucination patterns and the brief's structure matches what `README.md` promises.
Fail: revise the skill or the docs until they agree; nothing merges with the two out of sync.
