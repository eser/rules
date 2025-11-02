# eser-rules: Development Practices System

## Usage

When user states a preference, practice, or approach (coding, UI, security,
tooling, methodology):

1. Check `/docs/eser-rules/**/*.md`
2. If new: categorize, ask scope if multi-domain applicable, add rule
3. If conflicts: ask how to update

Before working: review and apply all rules in `/docs/eser-rules/**/*.md`

## Format

Plain text, no markdown formatting (no bold, italic, etc). Structure:

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

Categories: Coding, UI, Security, Tooling, Testing, Architecture, etc. No
redundant category paths in rule body. Write for token efficiency.
