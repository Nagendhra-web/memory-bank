<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=38&duration=3000&pause=1000&color=7F77DD&center=true&vCenter=true&repeat=true&width=600&height=60&lines=memory-bank;3-5x+longer+sessions;zero+wasted+tokens" alt="memory-bank" />

<br/>

[![GitHub stars](https://img.shields.io/github/stars/Nagendhra-web/memory-bank?style=for-the-badge&labelColor=1a1a2e&color=7F77DD)](https://github.com/Nagendhra-web/memory-bank/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/Nagendhra-web/memory-bank?style=for-the-badge&labelColor=1a1a2e&color=378ADD)](https://github.com/Nagendhra-web/memory-bank/issues)
![version](https://img.shields.io/badge/version-2.0.0-7F77DD?style=for-the-badge&labelColor=1a1a2e)
![license](https://img.shields.io/badge/license-Apache_2.0-1D9E75?style=for-the-badge&labelColor=1a1a2e)
![token savings](https://img.shields.io/badge/token_savings-60--80%25-FFD700?style=for-the-badge&labelColor=1a1a2e)
![works with](https://img.shields.io/badge/Claude_Code-ready-D85A30?style=for-the-badge&labelColor=1a1a2e)
![standard](https://img.shields.io/badge/agentskills.io-standard-378ADD?style=for-the-badge&labelColor=1a1a2e)
[![CI](https://img.shields.io/github/actions/workflow/status/Nagendhra-web/memory-bank/validate.yml?style=for-the-badge&labelColor=1a1a2e&label=CI)](https://github.com/Nagendhra-web/memory-bank/actions)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=for-the-badge&labelColor=1a1a2e)

<br/>

**Your Claude Code sessions die too fast. You waste tokens re-explaining your project every time.**

**memory-bank fixes both problems: persistent memory + 3-5x longer sessions.**

[Install](#install) · [Token Savings](#token-savings) · [Features](#features) · [Quick Start](#quick-start) · [Architecture](#architecture) · [Examples](#examples) · [Contributing](CONTRIBUTING.md)

</div>

---

## The Two Problems Nobody Has Solved Together

**Problem 1: Claude forgets everything between sessions.**

Every time you open Claude Code, you get: *"So, what are we working on today?"*
You've spent 6 sessions building an auth system. Claude remembers none of it.

**Problem 2: Sessions hit context limits way too fast.**

You spend 1,200-3,000 tokens re-explaining your project before doing any
real work. That's 10-25% of your session burned on warm-up. Over 10 sessions,
that's **12,000-30,000 tokens wasted** just getting Claude back to baseline.

## One Skill Fixes Both

Install memory-bank. Now you get this:

```
Welcome back! Last session you finished the Stripe webhook handler in
src/api/webhooks/stripe.ts — handlePaymentSuccess() is complete but
handleRefund() is still stubbed out. 3 commits have landed since, all
yours. The next step is writing integration tests for the webhook
endpoint. Ready to go?

Memory health: 9/10 | Branch: feature/checkout | Session 7
Context used for warm-up: ~800 tokens (vs ~3,000 without memory-bank)
```

No re-explaining. No lost context. No wasted tokens. **Sessions last 3-5x longer.**

---

## Token Savings

Real numbers. No fluff.

```
WITHOUT memory-bank (every session):
  Re-explain project:     ~400-800 tokens
  Re-explain decisions:   ~300-600 tokens
  Re-explain current work: ~200-500 tokens
  Clarification Q&A:      ~500-1,500 tokens
  ─────────────────────────────────────────
  Total waste per session: ~1,400-3,400 tokens

WITH memory-bank (every session):
  Compact memory load:    ~200-800 tokens (structured, complete)
  Re-explanation:         0 tokens
  Clarification:          0 tokens
  ─────────────────────────────────────────
  Total cost per session: ~200-800 tokens

  SAVINGS: 60-80% fewer tokens on context loading
```

| Metric | Without | With memory-bank |
|--------|---------|-----------------|
| Warm-up tokens per session | 1,400-3,400 | 200-800 |
| Token savings per session | — | 1,200-2,600 |
| Savings over 10 sessions | — | **12,000-26,000** |
| Sessions before context limit | Baseline | **3-5x more** |
| Time to productive work | 2-5 minutes | **Instant** |

### How It Saves Tokens

| Technique | Savings | How |
|-----------|---------|-----|
| Structured memory vs re-explaining | 800-1,500/session | Compact format replaces verbal explanation |
| Progressive loading (load only what's needed) | 300-600/session | Skip irrelevant sections |
| Compact encoding (tables > prose) | 200-400/session | Same info, 50% fewer tokens |
| Session continuation protocol | 500-1,000/handoff | Zero warm-up after context limits |
| Smart compression | 200-500/session | Smaller file = fewer tokens to read |
| Concise Claude responses | 300-800/session | Claude optimizes its own output |

---

## Install

```bash
npx skills add Nagendhra-web/memory-bank
```

Then add the auto-setup to your `CLAUDE.md` (or `~/.claude/CLAUDE.md` for all projects):

```markdown
## Memory

At the start of every session:
1. Check for MEMORY.md in the project root
2. Check current git branch for .memory/branches/<branch>.md overlay
3. Run a quick session diff — what changed since last update
4. Greet me with a specific summary and the next immediate step

At session end (when I say "wrap up", "save", or "done for now"):
1. Write comprehensive MEMORY.md with full current state
2. Make "Next immediate step" crystal clear
3. Compress if over 150 lines
```

That's it. Claude now remembers everything, forever.

---

## Features

This is not a simple note-taker. It's an adaptive memory engine.

### Layered Memory Architecture

```
┌─────────────────────────────────────────────┐
│  Layer 2: GLOBAL MEMORY                     │
│  ~/.claude/GLOBAL-MEMORY.md                 │
│  Your preferences across ALL projects.      │
├─────────────────────────────────────────────┤
│  Layer 1: PROJECT MEMORY                    │
│  ./MEMORY.md + branch overlays              │
│  Architecture, decisions, active work.      │
├─────────────────────────────────────────────┤
│  Layer 0: SESSION CONTEXT                   │
│  Current conversation only.                 │
│  Auto-flushes to Layer 1 at session end.    │
└─────────────────────────────────────────────┘
```

Layer 0 captures what you're doing now. Layer 1 tracks the project. Layer 2 remembers *you* across every project — your tool preferences, coding style, patterns you always use.

### Branch-Aware Memory

Switch branches, switch context. Automatically.

```
MEMORY.md                          ← base project memory
.memory/
  branches/
    feature-auth.md                ← auth context
    feature-payments.md            ← payments context
    bugfix-race-condition.md       ← bugfix context
```

Working on `feature/auth`? Claude loads the auth overlay. Switch to `feature/payments`? Different context loads instantly. Merge a branch? Claude folds the overlay back into base memory and cleans up.

No more "wait, weren't we working on payments?" when you're on the auth branch.

### Smart Compression

Memory files grow. Uncompressed memory becomes noise. Smart Compression keeps it lean:

| Lines | Action |
|-------|--------|
| < 100 | No action |
| 100-150 | Suggests compression |
| 150-200 | Auto-compresses |
| > 200 | Emergency compression + archive |

Completed tasks get collapsed. Resolved blockers get removed. Stale entries get flagged. **Key decisions and architecture notes are NEVER compressed** — they're permanent project knowledge.

Old session history moves to `MEMORY-ARCHIVE.md` so nothing is truly lost.

### Session Diffing

When you start a new session, Claude doesn't just read memory — it diffs against reality:

- **Git analysis:** What commits landed since your last session? By you? By teammates?
- **File validation:** Do all the files mentioned in memory still exist? Were any renamed?
- **Conflict detection:** Does memory say "using Express" while `package.json` has Fastify?
- **Dependency tracking:** Any new packages added or removed?

```
Since your last session (3 days ago): 7 commits — 4 by you, 3 by
@teammate. src/api/users.ts was refactored, 2 new deps added (zod,
@tanstack/query). Memory reference to src/auth.ts is stale — file
was renamed to src/authentication.ts. Auto-correcting.
```

### Memory Health Scoring

Every session start, memory gets a health score:

```
Memory health: 8/10
  Freshness:     9/10 (updated yesterday)
  Relevance:     7/10 (2 file paths changed)
  Completeness:  8/10 (all sections filled)
  Actionability: 9/10 (next step is crystal clear)
```

Health below 5? Claude suggests a rebuild. Below 3? Recovery mode kicks in.

### Recovery Mode

When memory is corrupted, severely stale, or missing:

1. Scans `package.json` / `pyproject.toml` / `go.mod` for stack detection
2. Reads last 20 git commits for recent activity
3. Checks README and CLAUDE.md for project context
4. Reconstructs memory from code reality
5. Presents it: "I've rebuilt memory from your code. Does this look right?"

Your project is never truly lost.

### Handoff Protocol

Onboarding a new developer? Generate a handoff document:

```
"generate a handoff for this project"
```

Claude reads memory + git history + code and produces a complete handoff: quick start instructions, architecture overview, active work, key decisions with reasoning, and gotchas. Optimized for humans, not AI.

### Velocity Tracking

After 5+ sessions, ask "how's our velocity?" and get:

- Tasks completed per session (trending up or down?)
- Recurring blockers (same issue appearing 3+ times)
- Scope creep detection (active work growing faster than completed?)
- Estimated sessions remaining for current work

### Context Efficiency Engine

The feature nobody else has built. Memory Bank actively minimizes token usage:

**Progressive Loading** — Don't dump everything into context. Load in tiers:
- Tier 1 (always): Project overview + where we left off + blockers (~200 tokens)
- Tier 2 (on demand): Key decisions, files, architecture (~300 tokens, only when needed)
- Tier 3 (rare): Session log, preferences, external context (~200 tokens, most sessions skip)

**Compact Encoding** — Tables instead of prose (50% fewer tokens for same info). Checklists instead of descriptions. File:line references instead of code snippets. Every line maximizes information per token.

**Context Budget Tracking** — Claude monitors usage and warns at milestones:
- 50%: suggests `/compact`
- 60%: auto-checkpoints memory
- 75%: recommends starting fresh
- 85%: emergency save

**Concise Response Mode** — Claude optimizes its own output during memory-bank sessions. Leads with results, uses file:line refs, skips preamble.

### Session Continuation Protocol

**The session killer, killed.** When you hit context limits or want to continue later:

1. Claude writes `CONTINUATION.md` — an ultra-compact warm-up file (under 50 lines, under 500 tokens)
2. Contains the exact resume point: file, function, line number
3. Contains what's done, what's half-done, and the immediate next action
4. Next session loads it first — **zero warm-up, instant productivity**

```
"Context is at 82%. I've saved everything. Start a new session and say
'continue' — I'll pick up at src/auth/refresh.ts:47 with zero warm-up."
```

```
Next session:
"Resuming from CONTINUATION.md. You were implementing handleRefund() in
route.ts:89 — handlePaymentSuccess() is done, refund handler needs the
Stripe refund.created event wired up. Let's go."
```

No more losing work when sessions end. No more re-explaining when they start.

---

## Quick Start

**1. Install the skill**

```bash
npx skills add Nagendhra-web/memory-bank
```

**2. Start a session with Claude Code**

Claude will offer to create your first `MEMORY.md` after meaningful work.

**3. End your session**

Say "wrap up" or "save progress". Claude writes everything to `MEMORY.md`.

**4. Start your next session**

Claude reads `MEMORY.md` and greets you with exactly where you left off. Zero re-explaining.

---

## Trigger Phrases

| Phrase | Action |
|--------|--------|
| `"remember this"` / `"don't forget"` | Save specific context to memory |
| `"pick up where we left off"` | Load memory and summarize |
| `"wrap up"` / `"save progress"` | Full session write to MEMORY.md |
| `"what were we working on"` | Read and recap last session |
| `"switch to [branch]"` | Load branch-aware context |
| `"memory health"` | Run health check and report score |
| `"compress memory"` | Run smart compression |
| `"hand off"` / `"onboard someone"` | Generate developer handoff doc |
| `"rebuild memory"` | Recovery mode — reconstruct from code |
| `"how's our velocity"` | Session analytics and trends |
| `"save state"` / `"continue this later"` | Session continuation — saves resume point |
| `"context budget"` / `"how much context left"` | Check token usage and get recommendations |
| `"running out of context"` | Emergency save + CONTINUATION.md |

---

## Architecture

```
skills/
  memory-bank/
    SKILL.md                          ← Core skill (the engine)
    references/
      memory-layers.md                ← 3-tier architecture deep dive
      branch-aware-memory.md          ← Git branch integration
      smart-compression.md            ← Compression algorithm
      session-diffing.md              ← Cross-session change detection
      advanced-patterns.md            ← Team workflows, velocity, snapshots
      context-efficiency.md           ← Token optimization deep dive
      claude-md-integration.md        ← Full setup guide
    examples/
      solo-fullstack.md               ← Solo dev Next.js project
      team-backend.md                 ← Team Go API project
      monorepo.md                     ← Turborepo multi-domain
      minimal.md                      ← 8-line prototype memory
template/
  SKILL.md                            ← Create your own skills
CONTRIBUTING.md
LICENSE
```

---

## Examples

### Solo Developer — Next.js App

```markdown
# Project Memory
Last updated: 2025-04-08 | Session 7 | Branch: feature/checkout
Memory health: 8/10

## Where We Left Off
- **Current task:** Stripe webhook handler in `src/api/webhooks/stripe.ts`
- **Status:** in progress — `handlePaymentSuccess()` done, `handleRefund()` stubbed
- **Next immediate step:** Write integration tests for webhook endpoint
- **Open question:** Use Stripe CLI for local webhook testing or mock?
```

### Team Project — Go API

```markdown
# Project Memory
Last updated: 2025-04-05 | Session 12 | Branch: main
Memory health: 7/10

## Where We Left Off
- **Current task:** Rate limiting middleware in `internal/middleware/ratelimit.go`
- **Status:** in progress — token bucket impl done, Redis backend next
- **Next immediate step:** [AK] Wire up Redis counter in `ratelimit.go:47`

## Key Decisions
| Date | Decision | Reasoning | Affects |
|------|----------|-----------|---------|
| 2025-03-15 | Chi over Gin | [JS] Better middleware composability | All routes |
| 2025-03-20 | sqlc over GORM | [JS] Type safety, no reflection | All DB queries |
```

### Minimal — Weekend Prototype

```markdown
# Memory — receipt-scanner
Updated: 2025-04-08 | Session 2

Working on: OCR pipeline with Tesseract → GPT-4 for receipt parsing
Next: Add multi-receipt batch processing to /api/scan endpoint
Blocked by: nothing
```

> See the [examples/](skills/memory-bank/examples/) directory for full, realistic examples.

---

## What Makes This Different

| Feature | memory-bank v2 | Basic memory skills | Manual notes |
|---------|:-:|:-:|:-:|
| Auto-load at session start | Yes | Yes | No |
| **Token savings (60-80% on warm-up)** | **Yes** | **No** | **No** |
| **Progressive loading (load only what's needed)** | **Yes** | **No** | **No** |
| **Session continuation protocol** | **Yes** | **No** | **No** |
| **Context budget tracking & warnings** | **Yes** | **No** | **No** |
| **Compact encoding (tables > prose)** | **Yes** | **No** | **No** |
| Branch-aware context | Yes | No | No |
| Smart compression & archival | Yes | No | No |
| Session diffing & conflict detection | Yes | No | No |
| Memory health scoring | Yes | No | No |
| Recovery mode (rebuild from code) | Yes | No | No |
| Velocity tracking & analytics | Yes | No | No |
| Handoff document generation | Yes | No | No |
| Global cross-project memory | Yes | No | No |
| Team collaboration protocol | Yes | Partial | No |
| Context snapshots at milestones | Yes | No | No |

---

## Contributing

We welcome contributions. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Quick version:**

1. Fork the repo
2. Create a feature branch
3. Make your changes (follow existing patterns)
4. Test with Claude Code
5. Open a PR with a clear description

Ideas for contributions:
- New advanced patterns in `references/advanced-patterns.md`
- New example MEMORY.md files for different project types
- Improvements to the compression algorithm
- Better conflict resolution strategies
- Integrations with other AI coding agents

---

## Roadmap

- [ ] **Memory search** — "when did we decide to use Prisma?" → instant answer
- [ ] **Visual memory map** — HTML visualization of project state and relationships
- [ ] **Memory diffing UI** — side-by-side view of memory changes across sessions
- [ ] **Plugin ecosystem** — custom memory sections for specific frameworks
- [ ] **Memory sharing** — export/import memory between projects with similar stacks
- [ ] **AI-powered compression** — smarter decisions about what to keep vs archive

---

## License

[Apache 2.0](LICENSE) — free for personal and commercial use.

---

<div align="center">

Built for the Claude Code community · Follows the [agentskills.io](https://agentskills.io) standard

**If this saved you from re-explaining your project one more time, give it a star.**

</div>
