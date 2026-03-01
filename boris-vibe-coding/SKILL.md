---
name: boris-vibe-coding
description: Use when starting a vibe coding session or managing parallel AI agents for development - fleet management, plan-first execution, browser verification loops, shared team memory
---

# Boris-Style Vibe Coding

## Overview

Engineering discipline applied to AI-driven development. Run fleets of parallel agents, always plan before executing, verify through the browser (not by trusting Claude's word), encode every mistake into CLAUDE.md.

**Core principle:** "A wrong fast answer is slower than a right slow answer."

## When to Use

- Starting any non-trivial feature or session
- Multiple independent tasks that can run in parallel
- Any task with a UI component that needs verification

**Do NOT skip this for "quick" changes** — quick changes without planning/verification create the most rework.

## The 5-Part Workflow

### 1. Fleet Management (not serial chat)

Run 5–15 Claude sessions in parallel, not one after another:

```
Terminal tabs: 1 | 2 | 3 | 4 | 5
claude.ai/code: 5–10 additional sessions
```

- Number tabs, use system notifications to know when input is needed
- Treat AI as **distributed cognitive capacity**, not a single assistant
- Independent tasks → assign to separate sessions immediately

**Baseline violation:** Running tasks serially when they have no dependencies.

### 2. Plan Mode First (always)

```
Session start → Plan Mode → iterate until plan is good → switch to auto-accept → 1-shot execution
```

Never jump directly to code. Back-and-forth in Plan Mode costs nothing compared to rework.

**Baseline violation:** Jumping straight to implementation to "save time."

### 3. Shared CLAUDE.md (team memory)

- One CLAUDE.md checked into git, shared by entire team
- When Claude makes **any** mistake → add it to CLAUDE.md immediately
- Errors become team knowledge; they should never repeat

```markdown
# In CLAUDE.md:
## DO NOT
- Use `useEffect` for data fetching — use React Query instead
- Import from `../utils` — always use `@/utils` alias
```

**Baseline violation:** Noting the mistake mentally but not encoding it, causing the same error next session.

### 4. Browser Verification Loop (most important)

**Never trust Claude's self-report of "done."** Always verify through the browser.

```
Write code → start dev server → Claude opens browser → tests UI/UX
→ if wrong: fix code → reload → re-test → repeat until it actually works
```

Implementation with Playwright MCP (already configured):
1. Start dev server in background (`npm run dev &` or equivalent)
2. Use `browser_navigate` → `localhost:3000`
3. Use `browser_snapshot` (accessibility tree) or `browser_take_screenshot`
4. Interact: `browser_click`, `browser_type`, `browser_fill_form`
5. If UI is wrong → fix code → `browser_navigate` again → verify

**Do not stop until the browser confirms it works.**

**Baseline violation:** Treating successful compilation as "done." It's not done until the browser says it's done.

### 5. Model Selection

Default: **Opus + thinking enabled** for everything.

| Situation | Model |
|-----------|-------|
| Architecture decisions | Opus + thinking |
| Code generation | Opus + thinking |
| "Just a quick fix" | Still Opus + thinking |
| Simple file rename | Sonnet is fine |

Wrong answers = rework. Rework cost > token cost.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Starting new feature | Plan Mode first, always |
| Multiple independent tasks | Parallel fleet sessions |
| Claude says "it's done" | Browser verification loop |
| Claude makes a mistake | Document in CLAUDE.md immediately |
| Speed vs accuracy | Always choose accuracy (Opus) |
| Quick PR | Plan Mode → auto-accept → 1-shot → browser verify |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Serial sessions for independent tasks | Open parallel tabs, assign immediately |
| Skipping Plan Mode for "small" changes | Small changes cause the most rework |
| Trusting `npm run build` success as verification | Open the browser and click through it |
| Noting mistakes mentally | Write to CLAUDE.md before moving on |
| Using fast model to save time | Wrong answer is slower than slow answer |

## Red Flags — Stop and Reset

- "I'll just quickly write the code first"
- "It compiled, so it's working"
- "I'll add it to CLAUDE.md later"
- "This is too simple for Plan Mode"
- "Using Sonnet for this is fine"

**All of these have caused rework. Follow the workflow.**
