# eser-rules: Development Practices System

## Usage

When user states preference/practice/approach:
1. Check `/docs/eser-rules/**/*.md`
2. If new: categorize by scope and impact level, ask multi-domain applicability
3. If conflicts: ask how to update

Before working: review and apply all rules in `/docs/eser-rules/**/*.md`

## Organization

Structure by scope and impact:

```
architecture/     High-level system design (modules, structure, ADRs, testing)
design/           Design principles (pure functions, immutability, composition)
practices/        Coding practices (mindset, validation, error handling)
javascript/       JS/TS language specifics (syntax, types, modules, runtime)
tooling/          Tools and workflows (Deno, package managers)
ui/               Frontend/UI guidelines
security/         Security practices
```

Consolidate minor rules into broader files. Avoid single-rule files.

## Format

Plain text, no markdown formatting. Structure:

```
# CategoryName

## Subcategory

Scope: applicable context
Rule: concise statement

Correct:
example

Incorrect:
example
```

Write for token efficiency.
