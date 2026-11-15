# 🤖 ai-kit

> A mixed open-source toolkit for AI skills, prompts, agents, and tools.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## 📂 Structure

```
ai-kit/
├── skills/      # Antigravity / AGY agent skill files (SKILL.md format)
├── prompts/     # Reusable LLM prompt libraries (system, few-shot, chain-of-thought)
├── tools/       # Scripts and utilities that extend AI agents
├── agents/      # Agent definitions, personas, and configurations
└── docs/        # Guides, architecture notes, and usage documentation
```

---

## 🚀 Getting Started

Clone the repo and browse the category that fits your need:

```bash
git clone https://github.com/saleem-15/ai-kit.git
cd ai-kit
```

### Using a Skill (Antigravity / AGY)

Copy any skill folder from `skills/` into your global config:

```
~/.gemini/config/skills/<skill-name>/SKILL.md
```

Then it's auto-discovered and available in all your projects.

---

## 🗂️ Categories

| Folder | What goes here |
|--------|---------------|
| `skills/` | Antigravity SKILL.md files — teach the agent workflows and runbooks |
| `prompts/` | Markdown or text prompt templates for any LLM |
| `tools/` | Python / PowerShell / shell scripts that extend agents |
| `agents/` | Agent persona definitions, system prompts, full agent configs |
| `docs/` | How-tos, architecture diagrams, usage guides |

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

- Found a bug or have a prompt idea? [Open an issue](.github/ISSUE_TEMPLATE/bug_report.md)
- Want to add a skill or tool? [Submit a PR](.github/ISSUE_TEMPLATE/feature_request.md)

---

## 📄 License

[MIT](LICENSE) © saleem-15
