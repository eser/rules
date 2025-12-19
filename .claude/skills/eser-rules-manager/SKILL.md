---
name: eser-rules-manager
description: Manages development practice rules. Use when user states a preference, practice, or approach to add as a rule. Also use when user asks to add, modify, or categorize coding rules.
---

# eser-rules: Development Practices Manager

## Usage

When user states preference/practice/approach:
1. Check existing skills in `.claude/skills/`
2. If new: categorize by scope and impact level, ask multi-domain applicability
3. If conflicts: ask how to update

Before working: review and apply all rules in `.claude/skills/*/SKILL.md`

## Organization

Structure by scope and impact:

```
.claude/skills/
├── architecture-guidelines/   High-level system design (modules, structure, ADRs, testing)
├── design-principles/         Design principles (pure functions, immutability, composition)
├── coding-practices/          Coding practices (mindset, validation, error handling)
├── javascript-practices/      JS/TS language specifics (syntax, types, modules, runtime)
├── tooling-standards/         Tools and workflows (Deno, package managers)
├── ui/                        Frontend/UI guidelines (create when needed)
└── security/                  Security practices (create when needed)
```

Consolidate minor rules into broader sections. Avoid single-rule sections.

## Format

Plain text, no markdown formatting inside rules. Structure:

```
## Section Name

Scope: applicable context
Rule: concise statement

Correct:
example

Incorrect:
example
```

Write for token efficiency.

## Adding New Rules

1. Identify the appropriate skill based on scope
2. Add rule to existing section or create new section if needed
3. Follow the format: Scope, Rule, Correct/Incorrect examples
4. Keep rules concise and actionable
