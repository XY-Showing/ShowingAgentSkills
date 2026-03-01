---
name: vibe-research
description: Use when starting an academic research session, planning literature review, designing experiments, or managing a multi-stage research workflow - parallel search, ground-truth verification, research knowledge base
---

# Vibe Research

## Overview

Engineering discipline applied to academic research. The three failure modes that kill research quality: serial search (missing related work), interpretation without verification (trusting Claude's summary over the paper), and undocumented dead ends (repeating failed experiments).

**Core principle:** Claude is a synthesis tool, not an authority. Always verify claims against primary sources.

## When to Use

- Starting any research session (literature review, experiment planning, writing)
- Any stage where Claude summarizes papers, results, or findings
- Before committing to a research direction or experimental setup

**Do NOT skip for "quick literature checks"** — unverified summaries and serial searches create compounding errors.

## Workflow

### 1. Lock the Research Question First

Before any search or experiment, write `research_plan.md`:

```
- Research question (specific, testable)
- Hypotheses (what you expect and why)
- Evaluation metrics (defined before seeing results)
- Baselines (what you're comparing against)
- Scope boundaries (what this study does NOT claim)
```

Read it before every major decision. For long sessions, also keep `findings.md` for key paper notes and decisions — prevents goal drift across iterations.

**Why this matters:** Metrics defined after seeing results = p-hacking. Baselines chosen after seeing your method = cherry-picking. Lock both before you look.

### 2. Parallel Literature Search

Run independent searches simultaneously, not serially:

```
Agent 1: Keyword cluster A (e.g., "gender bias medical QA LLM")
Agent 2: Keyword cluster B (e.g., "fairness healthcare NLP benchmark")
Agent 3: Citation network of seed paper
Agent 4: Related datasets / benchmarks
```

Different sources in parallel: arXiv, Semantic Scholar, ACL Anthology, OpenAlex. Synthesize after all return — never wait for one before starting another.

### 3. Primary Source Verification

**Never trust Claude's interpretation.** Always go to the source.

```
Claude summarizes paper → read the actual numbers in the paper
Claude reports experiment result → check the metric in W&B / log file
Claude says "significant" → check p-value and CI yourself
Claude lists citations → verify each one exists and says what Claude claims
```

**Citation verification is mandatory. No exceptions.**

Claude hallucinates citations. For every paper Claude names:
- Confirm it exists (search arXiv / Semantic Scholar by title + authors)
- Open the actual PDF — do not trust the abstract
- Find the specific claim Claude attributes to it (table, page, section)
- Note the exact location: "[Author Year, Table 3, p.8]"

A citation that can't be verified to page level should not be used.

**EDA before statistics:**

```
1. Plot raw data distributions
2. Look at failure cases before aggregate metrics
3. Check for data leakage, label imbalance, demographic skew
4. Then run statistical tests
5. Then interpret
```

Aggregate metrics hide what matters. Never skip to interpretation.

**Forbidden shortcuts:**
- Do NOT report a metric without first plotting its distribution
- Do NOT call a result "significant" without p-value + CI + sample size
- Do NOT skip failure case analysis ("the average looks fine" is not enough)

### 4. Research Knowledge Base (RESEARCH.md)

One file checked into the project repo, shared across sessions:

```markdown
## Dead Ends (do not repeat)
- GPT-2 on MedQA: too small, results not publishable (tried 2026-01)
- WinoBias for medical domain: domain mismatch, reviewers will flag it

## Confirmed Findings
- Llama-3 shows 12% gap on female pronouns in clinical notes (our result)

## Key Papers (verified)
- [Author, Year, Venue] — one-line contribution summary
```

Every failed experiment → RESEARCH.md immediately. Negative results documented prevent the same mistake next week, next month, by a collaborator.

### 5. Model Selection

| Decision | Model |
|----------|-------|
| Research question formulation | Opus + thinking |
| Experimental design | Opus + thinking |
| Interpreting ambiguous results | Opus + thinking |
| Keyword generation | Sonnet is fine |
| Formatting bibliography | Sonnet is fine |

A flawed research design costs weeks of compute. Wrong fast reasoning is slower than right slow reasoning.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Starting research session | Write research_plan.md first |
| Literature search | Parallel agents, multiple keyword clusters |
| Claude names a paper | Verify it exists + verify the claim to page level |
| Claude says "results show X" | Check the actual metric / log / plot |
| Experiment failed | Document in RESEARCH.md immediately |
| Long session (>1hr) | Check research_plan.md — are you still on track? |
| About to run stats | EDA first: plot distributions, check failures |
| Choosing baselines | Lock baselines in research_plan.md before running your method |

## Tool Stack

| Stage | Tools |
|-------|-------|
| Literature search | arXiv API, Semantic Scholar API, pyalex (OpenAlex), ACL Anthology |
| Paper reading + RAG | PaperQA2 (precise citations, low hallucination) |
| Related work drafting | Storm (Stanford) — structure first, then fill |
| Experiment tracking | W&B or MLflow — ground truth for all metrics |
| Experiment search | AIDE — metric-guided tree search for ML experiments |
| Writing | `/20-ml-paper-writing` skill for venue-specific structure |

## Red Flags — Stop and Verify

- "Claude said this paper found X, so let's build on that"
- "The results look good" (without checking raw metrics)
- "I'll document this dead end later"
- "Let me search one more keyword before designing the experiment"
- "These baselines make sense" (chosen after seeing your method's results)
- "I remember what we decided — no need to check the plan"

**All of these introduce errors that compound. Stop and verify.**
