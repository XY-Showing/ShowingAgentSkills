---
name: vibe-research
description: Use when starting an academic research session, planning literature review, designing experiments, or managing a multi-stage research workflow - parallel search, ground-truth verification, research knowledge base
---

# Vibe Research

## Overview

Engineering discipline applied to academic research. Run parallel literature searches, design before experimenting, verify against raw data (never Claude's interpretation), encode every dead end into a persistent research log.

**Core principle:** "The data is the browser. Never trust Claude's summary — verify against the source."

## When to Use

- Starting any research session (literature review, experiment planning, writing)
- Multiple independent research questions that can be explored in parallel
- Any stage where Claude summarizes results, papers, or findings

**Do NOT skip this for "quick literature checks"** — unverified summaries and serial searches create compounding errors.

## The 5-Part Workflow

### 1. Fleet Search (not serial browsing)

Run parallel agents for independent research dimensions simultaneously:

```
Agent 1: Search keyword cluster A (e.g., "gender bias medical QA LLM")
Agent 2: Search keyword cluster B (e.g., "fairness healthcare NLP benchmark")
Agent 3: Search citation network of seed paper
Agent 4: Search related datasets / benchmarks
```

- Assign each agent a distinct keyword cluster or database
- Use different sources in parallel: arXiv, Semantic Scholar, ACL Anthology, OpenAlex
- Synthesize after all agents return — never wait for one before starting another

**Baseline violation:** Searching one keyword at a time, one database at a time.

### 2. Research Design First (pre-registration mindset)

Before searching literature or running experiments, lock down:

```
research_plan.md:
  - Research question (specific, testable)
  - Hypotheses (what you expect to find and why)
  - Evaluation metrics (defined before seeing results)
  - Baselines (what you're comparing against)
  - Scope boundaries (what this study does NOT claim)
```

Create `research_plan.md` at session start. Read it before every major decision.

For long sessions, also create `findings.md` (discoveries, key paper notes) to prevent goal drift — Claude forgets the original question by iteration 8.

**Why this matters:** Metrics defined after seeing results = p-hacking. Baselines chosen after seeing your method = cherry-picking. Define both before you look.

**Baseline violation:** Jumping straight to literature search before locking the research question.

### 3. Research Knowledge Base (RESEARCH.md)

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

**Baseline violation:** Keeping failed approaches in memory — guaranteeing they get repeated.

### 4. Ground Truth Verification Loop (most important)

**Never trust Claude's interpretation of results or papers.** Always verify against the source.

```
Claude summarizes paper → go read the actual numbers in the paper
Claude reports experiment result → check the actual metric in W&B / log file
Claude says "significant" → check p-value and confidence interval yourself
Claude lists citations → verify each citation exists and says what Claude claims
```

**EDA-First pattern** (equivalent to browser recon-first):

```
1. Plot raw data distributions first
2. Look at failure cases before aggregate metrics
3. Check for data leakage, label imbalance, demographic skew
4. Then run statistical tests
5. Then interpret
```

Never skip to interpretation. Aggregate metrics hide what matters.

**Forbidden shortcuts:**
- Do NOT report a metric without first plotting its distribution
- Do NOT call a result "significant" without showing p-value + confidence interval + sample size
- Do NOT skip failure case analysis ("the average looks fine" is not enough)

**Citation verification is mandatory. No exceptions.**
Claude hallucinates citations. For every paper Claude names:
- Confirm it exists (search arXiv / Semantic Scholar by title + authors)
- Open the actual PDF — do not trust the abstract alone
- Find the specific number/claim Claude attributes to it (table, page, section)
- Note the exact location: "[Author Year, Table 3, p.8]"

A citation that can't be verified to page level should not be used.

**Baseline violation:** Accepting Claude's paper summary or citation list without opening the original paper.

### 5. Accuracy Over Speed

Default: **Opus + thinking enabled** for research-critical decisions.

| Decision | Model |
|----------|-------|
| Research question formulation | Opus + thinking |
| Experimental design choices | Opus + thinking |
| Interpreting ambiguous results | Opus + thinking |
| Keyword generation for search | Sonnet is fine |
| Formatting bibliography | Sonnet is fine |

A flawed research design costs weeks of compute and rework. Wrong fast reasoning is slower than right slow reasoning.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Starting research session | Write research_plan.md first |
| Literature search | Fleet: parallel agents, multiple keyword clusters |
| Claude names a paper | Verify it exists + verify the claim |
| Claude says "results show X" | Check the actual metric / log / plot |
| Experiment failed | Document in RESEARCH.md immediately |
| Long session (>1hr) | Check research_plan.md — are you still on track? |
| About to run stats | EDA first: plot distributions, check failures |
| Choosing baselines | Lock baselines in research_plan.md before running your method |

## Tool Stack (by research stage)

| Stage | Recommended tools |
|-------|------------------|
| Literature search | arXiv API, Semantic Scholar API, pyalex (OpenAlex), ACL Anthology |
| Paper reading + RAG | PaperQA2 (precise citations, low hallucination) |
| Related work drafting | Storm (Stanford) — structure first, then fill |
| Experiment tracking | W&B or MLflow — ground truth for all metrics |
| Experiment search | AIDE — metric-guided tree search for ML experiments |
| Writing | `/20-ml-paper-writing` skill for venue-specific structure |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Serial literature search | Fleet: parallel agents per keyword cluster |
| Defining metrics after seeing results | Lock metrics in research_plan.md first |
| Trusting Claude's citation list | Verify every paper: exists + claim is accurate |
| Trusting Claude's result summary | Check raw numbers in logs / W&B |
| Skipping EDA | Plot distributions before running any statistics |
| Keeping failed experiments in memory | Write to RESEARCH.md before moving on |
| Goal drift in long sessions | Read research_plan.md before every major step |

## Red Flags — Stop and Verify

- "Claude said this paper found X, so let's build on that"
- "The results look good" (without checking raw metrics)
- "I'll document this dead end later"
- "Let me search one more keyword before designing the experiment"
- "These baselines make sense" (chosen after seeing your method's results)
- "I remember what we decided — no need to check the plan"

**All of these introduce errors that compound. Stop and verify.**
