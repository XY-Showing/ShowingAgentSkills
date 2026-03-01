# ShowingAgentSkills

A curated collection of Claude Code skills built from real-world developer workflows — not AI-generated templates.

## Philosophy

Most public skill repositories focus on **tool execution**: run Playwright, generate PDFs, push to GitHub. This repo focuses on **methodology**: *how* to think about and structure AI-assisted development sessions.

Skills here are:
- Derived from proven workflows used by actual practitioners
- Tested with RED-GREEN baselines before publishing (writing-skills TDD standard)
- Complementary to existing skill ecosystems, not duplicative

---

## Skills

### `boris-vibe-coding`

**The only public skill based on Boris Cherny's (Claude Code creator) actual development workflow.**

Boris Cherny, head of Claude Code at Anthropic, ships 100 PRs/week with a "surprisingly vanilla" setup. This skill encodes his methodology as an activatable Claude workflow.

#### Core Philosophy

> "Engineering discipline applied to AI-driven development."

Vibe coding ≠ casual prompting. Boris's approach treats AI as **distributed cognitive capacity** — a fleet of parallel agents, each with a clear mandate, operating under strict verification discipline.

| Principle | What it means |
|-----------|---------------|
| **Fleet, not chat** | Run 10–15 Claude sessions in parallel. Serial is waste. |
| **Plan Mode first** | Iterate on the plan until it's right, then 1-shot execute. |
| **CLAUDE.md as team memory** | Every mistake gets encoded. Errors should never repeat. |
| **Browser verification** | Never trust Claude's "done". The browser confirms it. |
| **Opus + thinking always** | A wrong fast answer is slower than a right slow answer. |

#### What makes it different from existing skills

After surveying 380+ skills across VoltAgent, ComposioHQ, superpowers-lab, daymade, Jeffallan, and the official Anthropic skills repo — no equivalent methodology skill exists.

| Existing skills | This skill |
|-----------------|------------|
| Tool execution (run browser, push git) | Session-level methodology |
| Single-task focus | Holistic workflow from start to verification |
| Parallel execution as a feature | Parallel fleet as a *philosophy* |
| Browser as a test runner | Browser as the **only** source of truth |

Browser tool skills (lackeyjb/playwright-skill, ComposioHQ/webapp-testing) cover execution but not the surrounding discipline.

#### Two enhancements over Boris's original workflow

**1. Session persistence files** (inspired by planning-with-files)

CLAUDE.md handles cross-session team memory. `task_plan.md` handles within-session working memory. Long sessions drift without a persistent reference.

```
task_plan.md   → session goals, phases, current step
findings.md    → research notes, decisions, API docs
```

**2. Recon-First browser verification** (inspired by ComposioHQ/webapp-testing)

Don't click blind. Snapshot the DOM first, locate element refs, then interact.

```
browser_snapshot() → wait_for_load_state() → locate refs → interact
```

#### Install

```bash
git clone https://github.com/XY-Showing/ShowingAgentSkills.git /tmp/showing-skills
cp -r /tmp/showing-skills/boris-vibe-coding ~/.claude/skills/
```

Then invoke with `/boris-vibe-coding` in any Claude Code session.

---

## Contributing

Skills accepted if they:
- Are derived from a real, verified workflow (cite the source)
- Are tested with a baseline scenario before writing (RED-GREEN standard)
- Fill a gap not covered by existing public skills
