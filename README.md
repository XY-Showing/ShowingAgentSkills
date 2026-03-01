# ShowingAgentSkills

A curated collection of Claude Code skills built from real-world developer and researcher workflows — not AI-generated templates.

## Philosophy

Most public skill repositories focus on **tool execution**: run Playwright, generate PDFs, call APIs. This repo focuses on **methodology**: *how* to think about and structure AI-assisted work sessions.

Skills here are:
- Derived from proven workflows used by actual practitioners (cited sources)
- Tested with RED-GREEN baselines before publishing (writing-skills TDD standard)
- Filling gaps not covered by existing public skill ecosystems

---

## Skills

### `boris-vibe-coding`

**The only public skill based on Boris Cherny's (Claude Code creator) actual development workflow.**

Boris Cherny, head of Claude Code at Anthropic, ships 100 PRs/week with a "surprisingly vanilla" setup. This skill encodes his methodology as an activatable Claude workflow.

#### Core Philosophy

> "Engineering discipline applied to AI-driven development."

| Principle | What it means |
|-----------|---------------|
| **Fleet, not chat** | Run 10–15 Claude sessions in parallel. Serial is waste. |
| **Plan Mode first** | Iterate on the plan until it's right, then 1-shot execute. |
| **CLAUDE.md as team memory** | Every mistake gets encoded. Errors should never repeat. |
| **Browser verification** | Never trust Claude's "done". The browser confirms it. |
| **Opus + thinking always** | A wrong fast answer is slower than a right slow answer. |

#### What makes it different from existing skills

After surveying 380+ skills across VoltAgent, ComposioHQ, superpowers-lab, daymade, Jeffallan, and the official Anthropic skills repo — no equivalent methodology skill exists. Browser tool skills (lackeyjb/playwright-skill, ComposioHQ/webapp-testing) cover execution but not the surrounding discipline.

| Existing skills | This skill |
|-----------------|------------|
| Tool execution (run browser, push git) | Session-level methodology |
| Single-task focus | Holistic workflow from start to verification |
| Parallel execution as a feature | Parallel fleet as a *philosophy* |
| Browser as a test runner | Browser as the **only** source of truth |

#### Two enhancements over Boris's original workflow

**1. Session persistence files** — `task_plan.md` handles within-session working memory. Long sessions drift without it.

**2. Recon-First browser verification** — Snapshot DOM first, locate element refs, then interact. One accurate interaction beats five failed attempts.

#### Install

```bash
git clone https://github.com/XY-Showing/ShowingAgentSkills.git /tmp/showing-skills
cp -r /tmp/showing-skills/boris-vibe-coding ~/.claude/skills/
```

Invoke with `/boris-vibe-coding` in any Claude Code session.

---

### `vibe-research`

**The only public methodology skill for AI-assisted academic research workflows.**

Generalizes the boris-vibe-coding philosophy to research: parallel literature search, pre-registration mindset, ground-truth verification against raw data, and a persistent research knowledge base. Grounded in a survey of 380+ existing tools and skills (PaperQA2, Storm, AIDE, AI Scientist, GPT Researcher, and the full Claude skills ecosystem).

#### Core Philosophy

> "The data is the browser. Never trust Claude's summary — verify against the source."

| Principle | Research equivalent |
|-----------|-------------------|
| **Fleet, not chat** | Parallel agents per keyword cluster / database |
| **Plan first** | `research_plan.md` with metrics defined before experiments |
| **Knowledge base** | `RESEARCH.md` — dead ends, verified findings, key papers |
| **Ground truth verification** | Raw data, logs, original PDFs — never Claude's interpretation |
| **Accuracy over speed** | Opus + thinking for experimental design and result interpretation |

#### What makes it different from existing tools

After surveying the full landscape of AI research tools:

| Existing tools | This skill |
|----------------|------------|
| GPT Researcher, Storm | Synthesis and writing, not session methodology |
| PaperQA2 | Precise citation RAG, not workflow discipline |
| AIDE | ML experiment search, not research planning |
| AI Scientist | Automated pipeline, not human-in-loop methodology |
| `/20-ml-paper-writing` | Paper structure, not research process |

No existing skill or tool addresses: parallel fleet search across keyword clusters, pre-registration mindset enforced at session start, negative result encoding to prevent repeated failures, or EDA-first verification discipline.

#### Three research-specific additions beyond vibe-coding

**1. Citation verification protocol** — Claude hallucinates citations. Every paper must be verified to page level before use.

**2. EDA-First analysis** — Plot distributions, inspect failure cases, check for data leakage *before* running statistics or reporting metrics.

**3. RESEARCH.md knowledge base** — Negative results encoded immediately. Dead ends documented prevent weeks of repeated work by you or collaborators.

#### Install

```bash
git clone https://github.com/XY-Showing/ShowingAgentSkills.git /tmp/showing-skills
cp -r /tmp/showing-skills/vibe-research ~/.claude/skills/
```

Invoke with `/vibe-research` in any Claude Code session.

---

## Contributing

Skills accepted if they:
- Are derived from a real, verified workflow (cite the source)
- Are tested with a baseline scenario before writing (RED-GREEN standard)
- Fill a gap not covered by existing public skills
