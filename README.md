# Devil's Advocate

**Objective alignment and deep claim verification for AI-assisted research.**

A Claude Code skill that acts as a ruthless truth filter on gathered research — triaging every claim as Verified, Plausible, Unverified, or Contradicted, stripping hallucinations, and outputting a clean brief you can actually build on.

---

## What It Does

When you run `/devilsadvocate` after a research phase, it:

1. **Identifies input** — finds research context in the current conversation, memory, or vault
2. **Self-checks for confabulation** — names its own biases before evaluating anything
3. **Triages every claim** — categorizes each assertion with a structured hallucination taxonomy
4. **Filters for simplicity** — challenges complexity bias and surfaces minimum viable approaches
5. **Outputs an Objective Alignment Brief** — a structured document separating signal from noise
6. **Hands off to the next step** — routes to brainstorm, planning, or further research

## Why This Exists

AI research tools generate confident-sounding output full of unverified claims, phantom specificity, and complexity bias. This skill is the adversarial layer that catches:

- **Vague authority** — "experts recommend" with no source
- **Phantom specificity** — exact numbers invented by the model
- **Hedged assertions** — "may", "could potentially" that dodge commitment
- **Recency inflation** — stale research presented as current
- **Consensus manufacturing** — "the community agrees" without evidence
- **Complexity bias** — pushing the most sophisticated solution when a simpler one works

## Claim Triage System

Every claim from research is categorized:

| Symbol | Category | Criteria |
|--------|----------|----------|
| `[V]` | **Verified** | Confirmed by 2+ independent sources with URLs/citations |
| `[P]` | **Plausible** | Single credible source, or matches known patterns |
| `[U]` | **Unverified** | No source cited, AI-generated filler, or "many experts say" |
| `[X]` | **Contradicted** | Sources disagree, or claim conflicts with known facts |

### Hallucination Taxonomy

When flagging `[U]` or `[X]` claims, the failure mode is classified:

| Type | Description |
|------|-------------|
| **Intrinsic** | Contradicts the source material it claims to draw from |
| **Extrinsic** | Adds information not present in any cited source |
| **Entity** | Wrong names, orgs, products, or versions |
| **Attribution** | Real fact attributed to wrong source |
| **Citation** | Fabricated URLs, DOIs, or paper titles |

## Output Format

The skill produces an **Objective Alignment Brief**:

```
## Objective Alignment: [TOPIC]

### Bias Self-Check
[What biases were identified before triage]

### Verified Context (build on this)
- [V] [Claim — source1, source2]

### Plausible Context (use with awareness)
- [P] [Claim — source] — Note: [what would confirm/deny this]

### Stripped (do not carry forward)
- [U] [Claim] — Type: [intrinsic/extrinsic/entity/attribution/citation] — Why: [reason]
- [X] [Claim] — Counter: [what actually appears true]

### Simplicity Check
- Research suggests: [complex approach]
  Simpler alternative: [what might actually work]
  Complexity justified if: [condition]

### Actual Requirements (what we know is true)
1. [Hard requirement grounded in verified context]

### Open Questions (verify before proceeding)
- [ ] [Thing we assumed but didn't confirm]

### Blind Spots (what the research didn't cover)
- [Missing perspective, edge case, or domain not represented]
```

---

## Installation

### Claude Code (CLI / Desktop / Web)

```bash
# Clone to your skills directory
git clone https://github.com/7alexhale5-rgb/devils-advocate.git ~/.claude/skills/devilsadvocate

# Or copy just the skill file
mkdir -p ~/.claude/skills/devilsadvocate
curl -o ~/.claude/skills/devilsadvocate/SKILL.md \
  https://raw.githubusercontent.com/7alexhale5-rgb/devils-advocate/main/skills/devilsadvocate/SKILL.md
```

### Manual Installation

1. Create `~/.claude/skills/devilsadvocate/`
2. Copy `skills/devilsadvocate/SKILL.md` into that directory
3. (Optional) Copy `skills/_perspectives/skeptic.md` for the lightweight automatic version

### Verify Installation

In Claude Code, type `/devilsadvocate` — it should trigger the skill.

---

## Usage

### Standalone (full claim triage)

```
# After running research
/devilsadvocate

# Or with explicit context
"Run devil's advocate on this research"
"Sanity check these findings"
"What's real here?"
"Is this overcomplicated?"
```

### Trigger Phrases

The skill activates on: `verify this research`, `objective alignment`, `devil's advocate`, `sanity check`, `what's real here`, `is this overcomplicated`.

---

## Architecture

This repo contains two complementary components:

### 1. `/devilsadvocate` (Standalone Skill)

The full-depth verification skill. Invoked explicitly when you need deep claim triage on research output. Runs in the main conversation context.

**Location:** `skills/devilsadvocate/SKILL.md`

### 2. Skeptic Perspective (Automatic)

A lightweight, always-on version that fires automatically during every pipeline step (build, review, plan, brainstorm, research). Runs as a background subagent.

**Location:** `skills/_perspectives/skeptic.md`

| | Skeptic (automatic) | /devilsadvocate (standalone) |
|---|---|---|
| **Invocation** | Automatic — every review | Manual — user invokes |
| **Input** | Code diffs + files | Research output + context |
| **Focus** | Code quality, necessity | Research claims, hallucinations |
| **Claim triage** | Light (patterns only) | Full taxonomy ([V]/[P]/[U]/[X]) |
| **Output** | 1-5 structured findings | Full objective alignment brief |

---

## Principles

- **No softening** — if the research is wrong, say it's wrong
- **No new research** — work only from what was gathered; if context is missing, say so
- **Bias toward simplicity** — simpler path is probably right until proven otherwise
- **Attack the inputs, not the person** — this is about what's true, not who did the work
- **Preserve verified context** — don't throw out good findings in pursuit of minimalism
- **Be specific** — "this claim is unverified" is useless; "this claim has no source and contradicts X" is useful
- **No implementation** — produces a verified context brief, nothing more

---

## Research Foundation

This skill was refined using:

- **ECHO Framework** (EA Forum) — self-confrontation debiasing
- **arxiv 2504.04141** — self-debiasing paper (confabulation self-check is the single most effective mechanism)
- **Deepchecks + Lakera** — hallucination taxonomy (5-type classification)

---

## Pipeline Integration

Devil's Advocate sits between research and planning in a typical workflow:

```
research → devil's advocate → brainstorm → plan → implement → review
```

After delivering the brief, it routes to:
- `/brainstorm-stack` for design/visual work
- `/planning-stack` for technical implementation
- Further `/research-stack` if critical claims remain unverified

---

## License

MIT

---

## Author

Built by [Alex Hale](https://github.com/7alexhale5-rgb) as part of the [PrettyFly.ai](https://prettyflyforai.com) tooling suite.
