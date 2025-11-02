# JavaScript/TypeScript Types

## String to Number Conversion

Scope: JS/TS
Rule: Use Number() for conversions. Makes intent clearer than unary + operator.

Correct:
```typescript
const value = Number(userInput);
const port = Number(process.env.PORT ?? "8000");
```

Incorrect:
```typescript
const value = +userInput;  // unclear intent
const port = +(process.env.PORT ?? "8000");
```

---

## Type Checking

Scope: JS/TS
Rule: Avoid typeof operator. Use instanceof or .constructor. typeof returns unexpected results (typeof null === 'object').

Correct:
```typescript
const value = [1, 2, 3];
if (value instanceof Array) { }
if (value.constructor === Array) { }

const date = new Date();
if (date instanceof Date) { }
```

Incorrect:
```typescript
if (typeof value === "object") { }  // true for arrays, objects, null
if (typeof obj === "object") { }  // true for null
```

Exception: Checking for undefined:
```typescript
if (typeof someVar === "undefined") { }  // acceptable
```

---

## Null vs Undefined

Scope: JS/TS
Rule: Prefer null over undefined. Makes intent explicit.

Correct:
```typescript
let user: User | null = null;

function findUser(id: string): User | null {
  return users.get(id) ?? null;
}
```

Incorrect:
```typescript
let user: User | undefined;

function findUser(id: string): User | undefined {
  return users.get(id);
}
```

---

## Truthy/Falsy Checks

Scope: JS/TS
Rule: Avoid truthy/falsy checks unless boolean type. Use full conditions.

Correct:
```typescript
if (array.length === 0) { }
if (user !== null) { }
if (value !== 0) { }
if (isActive) { }  // boolean type
```

Incorrect:
```typescript
if (!array.length) { }  // false for length 0
if (user) { }  // false for null, undefined, 0, ""
if (value) { }  // false for 0, "", null, undefined
```
