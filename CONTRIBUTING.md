# Contributing to ai-kit

Thanks for your interest in contributing! Here's how to get started.

## How to Contribute

1. **Fork** the repo and create your branch from `main`
2. **Add** your skill, prompt, tool, or agent in the right folder
3. **Follow** the structure conventions below
4. **Open a Pull Request** with a clear description

## Conventions

### Skills (`skills/<name>/`)
- Must contain a `SKILL.md` with valid YAML frontmatter (`name`, `description`)
- Include a brief example or usage note at the top

### Prompts (`prompts/<category>/`)
- One `.md` or `.txt` file per prompt template
- Include a header comment explaining the use case and target model

### Tools (`tools/<name>/`)
- Include a `README.md` explaining what it does and how to run it
- Scripts should work cross-platform where possible

### Agents (`agents/<name>/`)
- Include a `README.md` with the agent's purpose, model recommendation, and usage

## Code of Conduct

Be respectful, constructive, and inclusive. This is a learning and sharing space.
