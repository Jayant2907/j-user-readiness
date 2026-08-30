# j-user-readiness

> **Agent Harness** — a visual demo-readiness harness for Cursor and Claude Code.

A **visual-readiness harness** for comprehension review of a screen: can someone who has never seen it understand it in ten seconds, and would you put it in front of a buyer?

Compatible with **Claude Code** and **Cursor** (both use a `SKILL.md` skill folder).

## What this skill does

`j-QA` asks "does it work and is it true?" This sibling asks the opposite: **is the screen demo-ready and understandable?** A screen can pass every `j-QA` rung and fail every item here.

The skill:

- **Measures, doesn't vibe** — reads real type sizes, widths, grouping, and state markers from source
- Fills every form with **realistic values** before scoring (empty forms hide hierarchy problems)
- Scores **24 checks** (PASS / WEAK / FAIL) across typography, grouping, density, state, and demo-readiness
- Hunts the **cross-cutting root cause** (shared tokens, default caption size, independent panel widths) before proposing per-screen patches
- Ends in one published **before/after artifact** plus a handover message a build agent can act on

## When to use it

Invoke when you say `j-user-readiness`, `how does this look`, `make it demo-ready`, `the screen is confusing`, `review the UI design`, or ask for fonts, sections, colours, spacing, or panel width to be improved.

## Install

### Cursor

**User-level:**

```bash
git clone https://github.com/Jayant2907/j-user-readiness.git ~/.cursor/skills/j-user-readiness
```

Windows (PowerShell):

```powershell
git clone https://github.com/Jayant2907/j-user-readiness.git "$env:USERPROFILE\.cursor\skills\j-user-readiness"
```

**Project-level:**

```bash
git clone https://github.com/Jayant2907/j-user-readiness.git .cursor/skills/j-user-readiness
```

### Claude Code

**User-level:**

```bash
git clone https://github.com/Jayant2907/j-user-readiness.git ~/.claude/skills/j-user-readiness
```

Windows (PowerShell):

```powershell
git clone https://github.com/Jayant2907/j-user-readiness.git "$env:USERPROFILE\.claude\skills\j-user-readiness"
```

**Project-level:**

```bash
git clone https://github.com/Jayant2907/j-user-readiness.git .claude/skills/j-user-readiness
```

Alternatively, copy the folder (it must contain `SKILL.md`) into the same locations.

Restart the agent session so the skill is picked up.

## How to run it

- `Run j-user-readiness on this screen`
- `Make this UI demo-ready`
- `The screen is confusing — review hierarchy and spacing`

Point the agent at the screen (URL or route) and, if possible, a running app with real data.

## What's in this repo

```
j-user-readiness/
├── SKILL.md    # Measurement rules + 24 checks + output
└── README.md
```

## Agent Harness collection

Part of the **Agent Harness** suite by [@Jayant2907](https://github.com/Jayant2907) — installable skills that wrap structured agent workflows (review harnesses, QA harnesses, impact sweeps) for Cursor and Claude Code.

| Harness | Role |
|---|---|
| [adversarial-review](https://github.com/Jayant2907/adversarial-review) | Merge-review harness |
| [p-code-review](https://github.com/Jayant2907/p-code-review) | Whole-codebase review harness |
| [feature-impact-sweep](https://github.com/Jayant2907/feature-impact-sweep) | Cross-cutting impact harness |
| [j-QA](https://github.com/Jayant2907/j-QA) | Manual UI QA harness |
| [j-user-readiness](https://github.com/Jayant2907/j-user-readiness) | Visual demo-readiness harness (this repo) |
| [j-module-audit](https://github.com/Jayant2907/j-module-audit) | Field-level module audit harness |
