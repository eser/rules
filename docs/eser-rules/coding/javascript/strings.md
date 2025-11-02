# JavaScript/TypeScript String Operations

## Substring Methods

Scope: JS/TS Rule: Use slice() instead of substring() or substr(). substr() is
deprecated and substring() has confusing parameter behavior.

Correct:

```typescript
const text = "Hello World";
const result = text.slice(0, 5); // "Hello"
const end = text.slice(6); // "World"
const last = text.slice(-5); // "World" (from end)
```

Incorrect:

```typescript
const text = "Hello World";
const result = text.substring(0, 5); // avoid
const end = text.substr(6); // deprecated
```
