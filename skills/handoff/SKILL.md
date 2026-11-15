---
name: handoff
description: Generates a zero-file, single-click copyable in-chat handoff payload engineered for parallel agent sessions and Git worktrees.
---

# Session Handoff Protocol (In-Chat / Worktree-Safe)

When the user invokes `/handoff` (or asks to pause/transfer the session), generate a single self-contained handoff block directly in the chat.

## Step 1: Gather Ground Truth (Read-Only)
1. **Inspect Worktree & Git State:** Run `pwd`, `git rev-parse --show-toplevel`, `git branch --show-current`, `git status -sb`, `git diff HEAD --stat`, and `git log -n 2 --oneline`.
2. **Strict No-File Rule:** Do **NOT** create, modify, or overwrite `HANDOFF.md` or any file on disk. Leave the working tree untouched.
3. **Repo-Relative Pointers Only:** Always format file references relative to the repo root (`path/to/file.ext:line`). Never use absolute filesystem paths for file pointers, as the next session may run in a different worktree.
4. **Zero Secrets:** Redact all API keys, tokens, credentials, and `.env` values.

## Step 2: Scale Depth to Task Scope
- **Quick Pause (1-2 files / minor fix):** Include ONLY the Header, Section 1, Section 2, and Section 5 (under 20 lines total).
- **Deep Handoff (Multi-file feature / complex refactor):** Include all 5 sections below.

## Step 3: Output a Single Copy-Paste Payload in Chat
- Output **nothing** outside the outer code block—no intro or outro text.
- **CRITICAL FORMATTING RULE:** Never use triple backticks (` ``` `) inside the payload, as nested fences break the chat UI's single-click copy button. Use single inline backticks (`` ` ``) for all commands, paths, and symbols.

````markdown
You are resuming an in-progress task from a previous session.
1. Run `pwd`, `git branch --show-current`, and `git status -sb` first. Compare against the Source Worktree and Branch below—if you are in a different worktree, edit files relative to YOUR current worktree root (never modify files via the old worktree's absolute path).
2. Run the `Verify First` command in Section 5 before editing any files.
3. Respect all constraints and dead ends in Sections 3 & 4, then execute `Next Step 1`.

# Handoff: [Task Name]
- **Source Worktree:** `[exact pwd path]`
- **Branch / Base:** `[current-branch]` (HEAD: `[short-commit-hash]`)
- **Working Tree State:** `[Clean | Dirty: tracked WIP | Dirty: includes untracked files]`

## 1. Objective & Done Criteria
- **Goal:** [1-2 sentences on what we are building/fixing]
- **Done Criteria:** [Exact test, build check, or observable behavior required]

## 2. Current State (Verified)
- **Completed:**
  - `repo/relative/path.ext` — [1-line summary of completed change]
- **In Progress (Resume Here):**
  - `repo/relative/path.ext:line` — [Exact state and what remains]
- **Untracked / Uncommitted Note:** [None, or list any uncommitted/untracked files that only exist in Source Worktree]

## 3. Decisions & Scope Boundaries (Do Not Undo)
- **Scope Guard (Stay in Lane):** Only modify `[allowed dirs/files]`. Do not touch `[out-of-bounds dirs/files being handled in other worktrees/PRs]`.
- **[Decision Made]:** [Brief rationale so the next agent does not revert it]

## 4. Dead Ends (Do Not Repeat)
- **[Approach Tried]:** Failed because `[exact error or limitation]`.

## 5. 30-Second Sanity Check & Next Step
- **Verify First:** `[exact single-line test, typecheck, or git command]`
- **Expected Output:** `[pass / specific current failure]`
- **Next Step 1:** [Single concrete action to take immediately after verification]
- **Next Step 2:** [Immediate follow-up action]