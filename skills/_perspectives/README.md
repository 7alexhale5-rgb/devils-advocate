# Perspectives

Shared analysis perspectives for skill pipelines. Each perspective defines a focused subagent role that can be spawned by any skill for parallel analysis.

## Included Perspective

| Name | File | Focus | Default Model | Always Fire? |
|------|------|-------|---------------|-------------|
| skeptic | `skeptic.md` | Devil's advocate — challenges assumptions, questions necessity, flags sloppiness | haiku | **Yes — every skill, every depth** |

The **skeptic** fires in every pipeline skill at every depth level:

| Skill | What the skeptic reviews |
|-------|------------------------|
| **Research** | Are the sources credible? Is the research over-complicated? |
| **Brainstorm** | Are we solving the right problem? Is the scope justified? |
| **Planning** | Is the plan earning its complexity? Are assumptions validated? |
| **Build** | Is the code sloppy? Does it match the stated intent? |
| **Review** | Is the implementation value-based? Are we shipping quality? |

## Spawn Pattern

Skills spawn perspectives using this pattern:

```
Agent:
  model: "{default_model}"
  run_in_background: true
  prompt: |
    You are a {name} analyst reviewing {context description}.

    Read the perspective definition for your focus areas and rules.

    ## Context
    {CONTEXT_PAYLOAD}

    ## Output Format Override
    Use the **{Code|Brainstorm|Research} Format** from your perspective file.

    ## Rules
    - Return ONLY structured findings as markdown
    - Max 5 findings, prioritized by severity
    - If you find nothing noteworthy, return "No findings."
    - No preamble, no summary, no conversation
  description: "{name} perspective"
```

## Escalation Pattern

After collecting results, the orchestrator checks quality:

```
IF perspective returned 0 findings on a non-trivial diff (50+ lines):
  -> Retry with escalation_model (sonnet)
  -> Prompt addition: "The initial review found nothing. Look harder —
     false negatives are worse than false positives."

IF retry also returns 0:
  -> Accept as clean. Note in report: "{name}: clean (verified 2x)"
```

## Depth Gating

Skills control how many perspectives fire based on their `--depth` flag. The skeptic always fires at every depth, including `--quick`, `--shallow`, and BUGFIX depths.

| Depth | Perspectives |
|-------|-------------|
| `--quick` / `--shallow` / BUGFIX | skeptic only |
| default | skeptic + top 2-3 most relevant |
| `--deep` / LARGE | skeptic + all applicable perspectives |

## Design Principles

- **Read-only**: Perspectives analyze and report. They never modify code.
- **Scoped**: Each perspective has a narrow focus. Overlap is expected — dedup happens at synthesis.
- **Capped**: Max 5 findings per perspective. Forces prioritization.
- **Structured**: Output follows a strict format so the orchestrator can merge across perspectives.
- **Isolated**: Each perspective runs in its own agent context. No cross-perspective dependencies.
