# Operators

## Null Handling

Scope: All languages with nullish coalescing (JS, TS, C#, Swift, Kotlin) Rule:
Use ?? for defaults. Coalesces only on null/undefined, not falsy values (0, "",
false).

Correct:

```typescript
const value = userInput ?? "default";
const port = config.port ?? 8000;
```

Incorrect:

```typescript
const value = userInput || "default"; // fails if userInput is ""
const port = config.port || 8000; // fails if port is 0
```
