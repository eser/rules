# eser/rules

![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)

A collection of reusable AI coding assistant instructions designed to work across tools like Claude Code, Cursor, and GitHub Copilot.

Think of it as [Context7](https://context7.com/) for your own codebase—a living memory that captures your team's coding conventions, architectural decisions, and best practices. As you and your contributors work on the codebase, these rules evolve with you: learning new patterns, embracing better conventions, and asking to be updated when things change.

For teams, it's a standardization layer that travels with your repository. Every contributor—human or AI—works from the same playbook, ensuring consistency across pull requests, code reviews, and refactors.

## Background

This repository started as a personal solution to a common problem: copy-pasting the same instructions between projects when working with AI coding assistants.

What began as a set of Cursor instructions evolved into a standardized, reusable format—validated when Anthropic introduced [Skills](https://code.claude.com/docs/en/skills) and GitHub Copilot adopted similar conventions. These developments confirmed that a portable instruction system isn't overengineering; it's the direction the ecosystem is heading.

## How It Works

Claude Code and GitHub Copilot natively recognize the `.claude/skills/` directory—no setup required. For other platforms, a simple directive in `AGENTS.md` or `.cursorrules` points the AI to your skills.

Once connected, the **eser-rules-manager** skill takes over. It acts as the orchestrator: guiding how rules are maintained, suggesting updates when conventions evolve, and organizing instructions so they stay coherent as your codebase grows. You focus on coding; it keeps the rules in sync.

## Compatibility

These skills work with tools that support the `.claude/skills` directory format:

| Tool | Support | Documentation |
|------|---------|---------------|
| Claude Code | ✅ | [Agent Skills](https://code.claude.com/docs/en/skills) |
| GitHub Copilot | ✅ | [Changelog announcement](https://github.blog/changelog/2025-12-18-github-copilot-now-supports-agent-skills/) |
| Cursor | ✅ | Via `.cursorrules` |
| Other Agents | ✅ | Via `AGENTS.md` |

## Installation

**Fresh install** (no existing skills):
```bash
npx degit eser/rules/.claude/skills .claude/skills
```

**Merge with existing skills**:
```bash
npx degit eser/rules/.claude/skills /tmp/eser-rules-skills
cp -r /tmp/eser-rules-skills/* .claude/skills/
rm -rf /tmp/eser-rules-skills
```

This copies each skill folder into your existing `.claude/skills/` directory without overwriting your current skills.

<details>
<summary>Alternative methods</summary>

**macOS / Linux**
```bash
cp -r path/to/eser-rules/.claude/skills/* .claude/skills/
```

**Windows (PowerShell)**
```powershell
Copy-Item -Recurse path\to\eser-rules\.claude\skills\* .claude\skills\
```

</details>

## Integration

### Claude Code & GitHub Copilot

No additional configuration needed. Both tools automatically discover and use skills from the `.claude/skills/` directory.

### Cursor & Other Agents

Cursor and other AI agents require explicit instruction to recognize the skills. Add the following directive to your configuration file:

- **Cursor**: `.cursorrules`
- **Other agents**: `AGENTS.md`

Create the file in your project root if it doesn't exist, then add:
```
See .claude/skills/eser-rules-manager/SKILL.md first to understand the organization of how we maintain this codebase's conventions and practices. Then read and follow the instructions in .claude/skills/ directory.
```

If you have existing rules, simply append this directive to your current configuration.

## Contributing

These rules are meant to evolve. If you find a better pattern, spot an inconsistency, or want to add a new skill, contributions are welcome.

## License

[Apache-2.0](LICENSE)
