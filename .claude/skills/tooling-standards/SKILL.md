---
name: tooling-standards
description: Development tooling standards including Deno runtime, JSR package registry, and configuration files. Use when setting up projects, managing dependencies, or configuring build tools.
---

# Tooling Standards

## Deno Tooling

### Tooling Preference

Scope: JS/TS projects using Deno
Rule: Prefer Deno tooling. Don't use npm directly. Use deno install for packages. Use built-in formatter, linter, benchmarks, testing.

Correct:
```bash
deno install
deno fmt
deno lint
deno test
deno bench
deno task dev
```

Incorrect:
```bash
npm install
npm run format
npm run lint
npm test
npx vitest
```

---

### Configuration Files

Scope: JS/TS projects using Deno
Rule: Use package.json for dependencies and scripts. Use tsconfig.json for TypeScript. Use deno.json only for formatter/linter configuration.

package.json (dependencies and scripts):
```json
{
  "dependencies": {
    "react": "^19.0.0",
    "@std/path": "npm:@jsr/std__path@^1.0.0"
  },
  "scripts": {
    "dev": "deno run --allow-all main.ts",
    "test": "deno test --allow-all"
  }
}
```

tsconfig.json (TypeScript config):
```json
{
  "compilerOptions": {
    "jsx": "react-jsx",
    "strict": true
  }
}
```

deno.json (formatter/linter only):
```json
{
  "fmt": {
    "lineWidth": 80,
    "semiColons": true
  },
  "lint": {
    "rules": {
      "exclude": ["no-explicit-any"]
    }
  }
}
```

Incorrect (don't use deno.json for dependencies):
```json
{
  "imports": {
    "react": "npm:react@^19.0.0"
  },
  "tasks": {
    "dev": "deno run main.ts"
  }
}
```

---

## Package Registry

### Registry Preference

Scope: JS/TS projects
Rule: Prefer jsr.io as package registry. Configure .npmrc to support JSR packages in package.json.

.npmrc:
```
@jsr:registry=https://npm.jsr.io
```

package.json with JSR packages:
```json
{
  "dependencies": {
    "@std/path": "npm:@jsr/std__path@^1.0.0",
    "@std/fs": "npm:@jsr/std__fs@^1.0.0",
    "react": "^19.0.0"
  }
}
```

Install with:
```bash
deno install
```

Incorrect (without npm: prefix or registry config):
```json
{
  "dependencies": {
    "@std/path": "^1.0.0"
  }
}
```

---

### Package Selection Priority

Scope: JS/TS projects
Rule: Prefer JSR packages over npm when available. Use npm packages when no JSR alternative exists.

Correct (JSR available):
```json
{
  "dependencies": {
    "@std/path": "npm:@jsr/std__path@^1.0.0",
    "@std/assert": "npm:@jsr/std__assert@^1.0.0"
  }
}
```

Correct (no JSR alternative):
```json
{
  "dependencies": {
    "react": "^19.0.0",
    "react-dom": "^19.0.0"
  }
}
```
