# Package Registry

## Registry Preference

Scope: JS/TS projects Rule: Prefer jsr.io as package registry. Configure .npmrc
to support JSR packages in package.json.

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

## Package Selection Priority

Scope: JS/TS projects Rule: Prefer JSR packages over npm when available. Use npm
packages when no JSR alternative exists.

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
