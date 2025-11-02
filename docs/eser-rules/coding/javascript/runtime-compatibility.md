# JavaScript/TypeScript Runtime Compatibility

## Module Paths

Scope: JS/TS ES Modules (Node 20.11+, Deno, Bun) Rule: Use import.meta.dirname
over dirname(fromFileUrl(import.meta.url))

Correct:

```typescript
const root = projectRoot ?? import.meta.dirname;
```

Incorrect:

```typescript
import { dirname } from "@std/path";
import { fromFileUrl } from "@std/url";
const root = dirname(fromFileUrl(import.meta.url));
```

---

## Path Context Distinction

Scope: JS/TS (Deno, Node, Bun) Rule: Use import.meta for module paths, cwd() for
user context

Module-relative (package internals):

```typescript
const templateDir = new URL(`../templates/${name}/`, import.meta.url).pathname;
const configPath = join(import.meta.dirname, "config", "defaults.json");
```

User context (CLI working directory):

```typescript
export function buildCommand(options: { projectRoot?: string }) {
  const userDir = options.projectRoot ?? Deno.cwd();
  const userConfig = join(userDir, "config.ts");
}
```

---

## Optional Path Parameters

Scope: JS/TS (CLI tools, build systems, test utilities) Rule: Add optional
projectRoot?: string parameter. Enables testing without global state changes.

Correct:

```typescript
export async function analyzeComponents(
  srcDir: string,
  projectRoot?: string,
): Promise<Component[]> {
  const root = projectRoot ?? import.meta.dirname;
  // ...
}
```

Incorrect:

```typescript
export async function analyzeComponents(srcDir: string): Promise<Component[]> {
  const root = Deno.cwd(); // hardcoded, untestable
  // ...
}
```
