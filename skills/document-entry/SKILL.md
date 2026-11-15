---
name: document-entry
description: >-
  Generates a correctly structured README or catalog entry for the
  awesome-agent-skills hybrid registry. Handles three entry types:
  original, curated, and improved — each with proper attribution,
  improvement documentation, and curator framing.
---

# Document Entry — Hybrid Registry Protocol

When the user asks you to document a skill, tool, or workflow for their
`awesome-agent-skills` repository, follow this protocol exactly.

---

## Step 1 — Classify the Entry

Ask (or infer from context) which type this entry is:

| Type | When to use it |
|------|---------------|
| **`[CURATED]`** | The original is excellent as-is. You are linking to it and writing a curator's note. No files are copied. |
| **`[IMPROVED]`** | The original had a good idea but gaps, bugs, or missing guardrails. You edited or rewrote it. The source is credited and your changes are documented. |
| **`[ORIGINAL]`** | Built from scratch by the curator (saleem-15). No external source. |

---

## Step 2 — Gather Required Information

Before writing anything, confirm you have:

- **Entry name** (e.g. `handoff`, `pr-review`)
- **Entry type** (`CURATED` / `IMPROVED` / `ORIGINAL`)
- **Source URL** (required for `CURATED` and `IMPROVED`)
- **Original author / repo** (required for `CURATED` and `IMPROVED`)
- **License of the original** (required for `IMPROVED` — check the source repo)
- **What was changed** (required for `IMPROVED` — ask the user to describe it)
- **Why it was changed** (required for `IMPROVED`)
- **Curator's note** — the user's personal one-line take on why this entry matters

If any required field is missing, ask one short question at a time before proceeding.

---

## Step 3 — Write the Entry README

Use exactly this structure. Do not add sections. Do not remove sections.

```markdown
# [Entry Name]

> **Type:** [CURATED | IMPROVED | ORIGINAL]  
> **Trigger:** `/[trigger]` *(or describe how to invoke)*  
> **Compatible with:** [Claude Code | Google Antigravity | Cursor | Windsurf | All]

[One sentence: what this skill/tool does and when you reach for it.]

---

## Why It's in This Collection

> *[Curator's note — 2–3 sentences in first person. What engineering pain does
> it solve? Why did it earn a spot here over the alternatives?]*

---

## Source & Attribution

<!-- REQUIRED for CURATED and IMPROVED. Remove this section for ORIGINAL. -->

- **Original:** [repo-name](source-url) by [@author](author-profile-url)
- **License:** [MIT | Apache-2.0 | etc.] *(verify in the source repo)*
- **Entry type:** [Linked as-is | Forked and improved]

---

## What Was Improved *(IMPROVED entries only — delete for CURATED and ORIGINAL)*

> These are the specific changes made by [@saleem-15](https://github.com/saleem-15).
> The original work is credited above; these additions are documented here for
> transparency and so the next developer knows exactly what diverged.

- **[Change 1]:** [What changed and why — e.g. "Removed disk writes; replaced
  with in-chat clipboard payload to survive worktree switches."]
- **[Change 2]:** [What changed and why]
- **[Change 3]:** [What changed and why]

*The original `[repo-name]` remains the upstream reference. This version is a
 derivative work under the terms of its [LICENSE].*

---

## Install

```bash
# Google Antigravity (global)
cp -r skills/[entry-name] ~/.gemini/config/skills/[entry-name]

# Claude Code (global)
cp -r skills/[entry-name] ~/.claude/skills/[entry-name]
```

---

## How It Works

1. [Step 1 — what the user types or does]
2. [Step 2 — what the agent does internally]
3. [Step 3 — what the output looks like]

---

## Field Notes

📄 [`docs/[entry-name]-notes.md`](../../docs/[entry-name]-notes.md) — curator's
extended notes: what was tested, what broke, and what the tradeoffs are.

*(Create this file when you have enough hands-on experience with the entry.)*
```

---

## Step 4 — Write the Catalog Row

After writing the entry README, also output a one-line table row for the
root `README.md` catalog:

```markdown
| **[`entry-name`]([type-badge] ./skills/entry-name/)** | `/trigger` | [CURATED\|IMPROVED\|ORIGINAL] | One-line summary. |
```

Type badges:
- `CURATED` → no badge prefix needed
- `IMPROVED` → prefix the link label with `✏️`
- `ORIGINAL` → prefix the link label with `⭐`

---

## Step 5 — Attribution Rules (Non-Negotiable)

These rules apply to every `IMPROVED` entry without exception:

1. **Always name the original repo and author** in the Source & Attribution section.
2. **Always link to the original**, not just mention it.
3. **Always state the original's license** so the user knows if their modifications are legally compatible.
4. **Never describe an `IMPROVED` entry as "built by saleem-15"** — use "improved", "extended", "adapted", or "derived from" instead.
5. **Document every meaningful change** in the "What Was Improved" section — vague entries like "cleaned up" are not acceptable.
6. If the original has **no open-source license**, flag it explicitly:
   > ⚠️ *The upstream repo has no license. Redistribution of modified versions
   > may not be legally permitted. Curator's note only — no files copied.*

---

## What NOT to Do

- Do **not** write "I built this" or "created by saleem-15" for `CURATED` or `IMPROVED` entries.
- Do **not** omit the Source & Attribution section to make an `IMPROVED` entry look `ORIGINAL`.
- Do **not** copy source code from a GPL-licensed repo into an MIT-licensed entry without flagging the license conflict.
- Do **not** invent attribution details — if you don't know the license, say "verify in source repo."
