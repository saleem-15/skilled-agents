# AI Engineering Skills & Workflows

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A curated collection of production-tested skills, slash commands, and workflows for AI coding agents (**Claude Code**, **Google Antigravity**, **Cursor**, and **Windsurf**).

Most community prompts assume you work in a single chat window on a single branch. These skills are built around how parallel AI engineering actually works in practice: **multiple concurrent agent sessions, isolated Git worktrees, strict branch protections, and zero repo bloat.**

---

## Quick Install

Copy any skill folder from `skills/` into your global or project skills directory:

```bash
# Google Antigravity (global)
cp -r skills/handoff ~/.gemini/config/skills/handoff

# Claude Code (global)
cp -r skills/handoff ~/.claude/skills/handoff

# Or install via npx skills (works across Claude Code, Antigravity, Cursor, Windsurf)
npx skills add saleem-15/ai-kit/handoff
```

---

## Skills Catalog

| Skill | Trigger | Summary |
| :--- | :--- | :--- |
| **[`handoff`](#1-handoff--stateless-worktree-safe-session-handoff)** | `/handoff` | Zero-file, single-click clipboard handoff built for parallel sessions and Git worktrees. |
| *More coming soon...* | | |

---

## 1. `handoff` — Stateless, Worktree-Safe Session Handoff

📄 **Skill File:** [`skills/handoff/SKILL.md`](./skills/handoff/SKILL.md)

### Why We Built It

When an AI coding session approaches its context limit—or when you need to pause and spin up a fresh agent—you need a clean way to transfer state without starting from zero.

However, existing handoff skills write physical files like `HANDOFF.md` or `.claude/handoffs/*.md` directly to your disk. In a real-world workflow, file-based handoffs break down fast:

- **Parallel Session Collisions:** Running two or three agent chats at the same time overwrites or confuses a shared `HANDOFF.md` file.
- **Git Worktree Isolation:** If you create a handoff in `worktree-a` and spin up your next agent in `worktree-b`, an untracked local file isn't there.
- **Zero Bloat & Strict `main` Rules:** You shouldn't have to manually delete leftover handoff files, maintain `.gitignore` rules, or risk committing temporary agent notes to a protected branch.

### Inspiration & Credits

This skill stands on the shoulders of great open-source work in the agent community while taking a fundamentally different architectural path (stateless clipboard payload vs. disk files):

- **[REMvisual/claude-handoff](https://github.com/REMvisual/claude-handoff):** Inspired our **Dead Ends ("What We Tried")** section so the incoming session never wastes tokens repeating failed experiments.
- **[cskwork/handoff-skill](https://github.com/cskwork/handoff-skill) & [softaworks/agent-toolkit](https://github.com/softaworks/agent-toolkit):** Inspired the structured state packet and explicit resume contract.
- **Matt Pocock's Pointer-First Context Pattern:** Referencing `repo/relative/path.ext:line` instead of dumping raw code blocks into the handoff, keeping the new agent's context window lean.

### What Makes This Version Different

- **100% Stateless on Disk (In-Chat Payload):** Strictly forbids creating or modifying any files. The agent outputs a single self-contained block containing both the resume instructions and the state packet—ready to copy with one click.
- **Cross-Worktree Boundary Guards:** Records the exact source worktree (`pwd`), branch, and commit hash, but enforces **repo-root relative file pointers**. If you paste the handoff into a different worktree, the incoming agent knows to edit files in its *own* worktree rather than reaching back into the old directory's absolute path.
- **30-Second Sanity Gate:** Forces the incoming agent to run a concrete verification command (test, typecheck, or `git status -sb`) and confirm the baseline before touching a single line of code.
- **Stay-in-Lane Scope Guard:** Explicitly defines which directories are in-bounds and which are being modified by other concurrent sessions/worktrees to prevent merge conflicts.
- **UI-Safe Formatting:** Forbids nested triple-backticks inside the output payload so the chat UI never splits the copyable block in half.

### How It Works

1. Type `/handoff` (or ask the agent to wrap up the session).
2. The agent inspects `pwd`, `git status -sb`, `git diff HEAD --stat`, and recent commits in read-only mode.
3. It scales the output automatically — a compact 20-line brief for a quick pause, or a full 5-section brief for a deep multi-file refactor.
4. Click **Copy** once on the generated block, paste it into any new chat session across any worktree, and continue immediately.

---

## Template for Adding New Skills

Every skill in this repository follows the same lightweight documentation standard:

1. **Why We Built It** — The workflow friction it solves.
2. **Inspiration & Credits** — Prior art and community ideas we built upon.
3. **What Makes This Version Different** — Technical guardrails under the hood.
4. **How It Works** — Trigger and step-by-step flow.

---

## License

[MIT](LICENSE) © [saleem-15](https://github.com/saleem-15)
