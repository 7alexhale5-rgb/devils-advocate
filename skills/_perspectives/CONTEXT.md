# Perspectives room: the automatic skeptic perspective

One job: keep the always-on skeptic subagent (fires on every pipeline skill, every depth)
accurate to its spawn contract. Paths are relative to the repo root.

## Inputs

- The perspective definition: `skills/_perspectives/skeptic.md` (YAML frontmatter —
  `default_model: haiku`, `escalation_model: sonnet`, `escalation_trigger`, `always_fire: true`
  — plus the five core questions and output format).
- The spawn and escalation contract: `skills/_perspectives/README.md` § Spawn Pattern,
  § Escalation Pattern, § Depth Gating, § Design Principles (read-only, scoped, capped at 5
  findings, isolated per-agent context).
- Missing input: a change to the escalation trigger or depth-gating table with no matching
  update to `README.md`'s tables is incomplete.

## Process

1. Edit `skills/_perspectives/skeptic.md` — the core questions, the output format, or the
   frontmatter fields (`default_model`, `escalation_model`, `escalation_trigger`).
2. If the change affects when or how the skeptic spawns (depth gating, escalation retry,
   always-fire scope), update `skills/_perspectives/README.md` § Spawn Pattern / § Escalation
   Pattern / § Depth Gating tables in the same change.
3. NOT FOUND: no automated test exists in this repo — verification is manual, per Human check.

## Outputs

- Changed `skills/_perspectives/skeptic.md`.
- Matching edits to `skills/_perspectives/README.md` when the spawn or escalation contract
  changed.

## Human check

Alex reads a real pipeline run (build, review, plan, or brainstorm) where the skeptic fired and
checks: did it return at most 5 findings, in the stated format, with zero findings only after
the sonnet-escalation retry (per `escalation_trigger`)? Pass: the run matches the documented
contract. Fail: revise the perspective file or its README until the live behavior and the docs
agree.
