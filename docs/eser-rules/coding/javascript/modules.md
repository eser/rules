# JavaScript/TypeScript Module Patterns

## Exports

Scope: JS/TS Rule: Always use direct named exports with export keyword. Avoid
default exports.

Correct:

```typescript
export function buildCommand() {}
export const CONFIG_PATH = "./config";
export class UserService {}
export type BuildOptions = {};
```

Incorrect:

```typescript
function buildCommand() {}
const CONFIG_PATH = "./config";
export { buildCommand, CONFIG_PATH }; // indirect export

export default buildCommand; // default export
```

---

## Imports

Scope: JS/TS Rule: Prefer namespace imports to prevent naming collisions.

Correct:

```typescript
import * as path from "@std/path";
import * as fs from "@std/fs";

const filePath = path.join(dir, "config.ts");
const exists = await fs.exists(filePath);
```

Incorrect:

```typescript
import { join, resolve } from "@std/path";
import { copy, exists } from "@std/fs";

const filePath = join(dir, "config.ts"); // potential collision with other 'join'
```

Exception: Single function imports from small modules:

```typescript
import { assertEquals } from "@std/assert";
```

---

## Import Paths

Scope: JS/TS Rule: Use explicit file extensions and paths. Avoid sloppy imports.
Non-explicit specifiers are ambiguous and require probing for correct file path
on every run.

Correct:

```typescript
import { add } from "./math/add.ts";
import { ConsoleLogger } from "./loggers/index.ts";
import { buildConfig } from "../config/build.ts";
```

Incorrect:

```typescript
import { add } from "./math/add"; // missing extension
import { ConsoleLogger } from "./loggers"; // ambiguous directory import
import { buildConfig } from "../config/build"; // missing extension
```
