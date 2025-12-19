# eser/rules

A collection of reusable AI coding assistant instructions designed to work across tools like Claude Code, Cursor, and GitHub Copilot.

## Background

This repository started as a personal solution to a common problem: copy-pasting the same instructions between projects when working with AI coding assistants.

What began as a set of Cursor instructions evolved into a standardized, reusable format—validated when Anthropic introduced [Skills](https://code.claude.com/docs/en/skills) and GitHub Copilot adopted similar conventions. These developments confirmed that a portable instruction system isn't overengineering; it's the direction the ecosystem is heading.

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

## Usage

Once installed, Claude Code will automatically discover and use these skills based on context. You can also explicitly reference them:
```
Take a look at @.claude/skills/ and use the relevant instructions.
```

## Why Use This?

- **Consistency** — Same coding standards and patterns across all your projects
- **Portability** — Works with multiple AI tools without modification
- **Maintainability** — Update once, benefit everywhere

## License

[Apache-2.0](LICENSE)
