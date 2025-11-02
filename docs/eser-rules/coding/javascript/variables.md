# JavaScript/TypeScript Variables

## Variable Declaration

Scope: JS/TS Rule: Prefer const over let. Use const by default, only use let
when reassignment is required.

Correct:

```typescript
const userName = "John";
const config = { port: 8000 };
const items = [1, 2, 3];

let counter = 0;
counter++; // reassignment needed, let is appropriate
```

Incorrect:

```typescript
let userName = "John"; // never reassigned, should be const
let config = { port: 8000 }; // never reassigned, should be const
let items = [1, 2, 3]; // never reassigned, should be const
```

Note: const prevents reassignment, not mutation:

```typescript
const obj = { value: 1 };
obj.value = 2; // allowed, mutation not reassignment

const arr = [1, 2, 3];
arr.push(4); // allowed, mutation not reassignment

obj = { value: 2 }; // error, reassignment not allowed
```
