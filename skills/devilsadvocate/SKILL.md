---
name: devilsadvocate
description: Standalone deep verification of research claims and assumptions. Use outside the normal pipeline when you need full claim triage — "verify this research", "objective alignment", "devil's advocate", "sanity check", "what's real here", "is this overcomplicated". NOT part of the main workflow (the skeptic perspective handles that automatically).
---

# Devil's Advocate: Objective Alignment

You are executing an objective alignment pass on gathered research context. Your job is to be ruthlessly honest about what's verified, what's assumed, and what's noise — then output a clean brief that keeps things as simple as possible without restricting the build.

> **Standalone skill — NOT part of the main pipeline.** The skeptic perspective (`_perspectives/skeptic.md`) provides built-in devil's advocate analysis at every step of the pipeline automatically. Use this standalone `/devilsadvocate` when you need the **full claim triage** — hallucination taxonomy, source verification, simplicity filtering — on research output outside the normal workflow. Common use: after a research phase when you want deep verification before acting on findings.

---

## Step 1: Identify Input

Look for research context in this priority order:

1. **Current conversation** — if research was run this session, use its output
2. **Files or URLs** — if the user pointed to specific documents, use those
3. **No research found** — ask: "What context should I verify? Paste findings, point me to a file, or run your research pipeline first."

Extract every distinct claim, recommendation, or assertion from the research output.

---

## Step 1.5: Confabulation Self-Check

Before triaging claims, name your own biases about this research in a single paragraph:

- What am I predisposed to **agree with** because it confirms existing knowledge?
- What am I predisposed to **dismiss** because it's unfamiliar?
- Where might I be **pattern-matching** to something I "know" that doesn't actually apply here?

State these explicitly in the output. This prevents silent bias from contaminating the triage.

---

## Step 2: Claim Triage

Categorize every claim from the research into one of four buckets:

| Category | Criteria | Symbol |
|----------|----------|--------|
| **Verified** | Confirmed by 2+ independent sources with URLs/citations | `[V]` |
| **Plausible** | Single credible source, or matches known patterns | `[P]` |
| **Unverified** | No source cited, AI-generated filler, or "many experts say" style claims | `[U]` |
| **Contradicted** | Sources disagree, or claim conflicts with known facts | `[X]` |

### Hallucination Taxonomy

When flagging `[U]` or `[X]` claims, classify the failure mode:

| Type | What It Is |
|------|-----------|
| **Intrinsic** | Contradicts the source material it claims to draw from |
| **Extrinsic** | Adds information not present in any cited source |
| **Entity** | Wrong names, orgs, products, or versions |
| **Attribution** | Real fact attributed to wrong source |
| **Citation** | Fabricated URLs, DOIs, or paper titles |

### Hallucination Patterns to Flag

Strip or flag these patterns — they compound downstream if left unchecked:

- **Vague authority**: "experts recommend", "best practice is", "it's widely known" — WHO says this? WHERE?
- **Phantom specificity**: Exact numbers, dates, or version numbers with no source — AI loves inventing these
- **Hedged assertions**: "may", "could potentially", "is likely to" — either it does or it doesn't. Which is it?
- **Recency inflation**: "recently", "the latest trend" — when exactly? Is this from 2024 research being presented as current?
- **Complexity bias**: Research that pushes toward the most sophisticated solution when a simpler one exists
- **Consensus manufacturing**: "the community agrees" — does it? Show me the thread.

---

## Step 3: Simplicity Filter

For each recommendation or approach suggested by the research, ask:

1. **Is this actually needed?** Or is it interesting but irrelevant to what we're building?
2. **Is there a simpler way?** Research often surfaces the most comprehensive approach, not the most appropriate one.
3. **What's the minimum viable version?** Strip it down to the smallest thing that solves the actual problem.
4. **Who is this advice for?** A recommendation for a 50-person team may not apply to a solo builder.

The goal is NOT to reject complexity — it's to ensure complexity is justified by actual requirements, not research momentum.

---

## Step 4: Output — Objective Alignment Brief

Present findings in this format. No softening, no preamble.

```
## Objective Alignment: [TOPIC]

### Bias Self-Check
[Single paragraph from Step 1.5 — what biases were identified]

### Verified Context (build on this)
- [V] [Claim — source1, source2]
- [V] [Claim — source1, source2]

### Plausible Context (use with awareness)
- [P] [Claim — source] — Note: [what would confirm/deny this]
- [P] [Claim — source]

### Stripped (do not carry forward)
- [U] [Claim that was unsourced/hallucinated] — Type: [intrinsic/extrinsic/entity/attribution/citation] — Why: [reason]
- [X] [Claim that was contradicted] — Counter: [what actually appears true]

### Simplicity Check
- **Research suggests:** [complex approach]
  **Simpler alternative:** [what might actually work]
  **Complexity justified if:** [condition that would make the complex version necessary]

### Actual Requirements (what we know is true)
1. [Hard requirement grounded in verified context]
2. [Hard requirement]
3. [Hard requirement]

### Open Questions (verify before proceeding)
- [ ] [Thing we assumed but didn't confirm]
- [ ] [Thing that needs real-world validation]

### Blind Spots (what the research didn't cover)
- [Topic or angle the research should have addressed but didn't]
- [Missing perspective, edge case, or domain not represented]
- [Assumption baked in that was never questioned]
```

---

## Step 5: Pipeline Handoff

After delivering the brief:

### If design/visual oriented:
> "Context verified. Run your brainstorming workflow — this should go through visual prototyping."

### If technical/backend:
> "Context verified. Run your brainstorming workflow to explore decisions, then plan implementation."

### If critical open questions remain:
> "There are [N] unverified claims that could change the approach. Want to run more research on these specific questions first, or proceed with what we have?"

---

## Rules

- **No softening** — if the research is wrong, say it's wrong
- **No new research** — work only from what was gathered. If context is missing, say so.
- **Bias toward simplicity** — when in doubt, the simpler path is probably right until proven otherwise
- **Attack the inputs, not the person** — this isn't about whether the research was done well, it's about what's actually true
- **Preserve all verified context** — don't throw out good findings in pursuit of minimalism
- **Be specific** — "this claim is unverified" is useless. "This claim has no source and contradicts X" is useful.
- **No implementation** — this step produces a verified context brief, nothing more

## When NOT to Use

- When you already have high-confidence context and just want to build — skip to brainstorming
- When the task is trivial (<10 LOC) — skip the whole pipeline
- When you know what you want — go straight to planning
