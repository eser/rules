# JavaScript/TypeScript Syntax

## Variable Declaration

Scope: JS/TS
Rule: Prefer const over let. Use const by default, only use let when reassignment required.

Correct:
```typescript
const userName = "John";
const config = { port: 8000 };
let counter = 0;
counter++;  // reassignment needed
```

Incorrect:
```typescript
let userName = "John";  // never reassigned
```

Note: const prevents reassignment, not mutation:
```typescript
const obj = { value: 1 };
obj.value = 2;  // allowed
obj = { value: 2 };  // error
```

---

## Semicolons

Scope: JS/TS
Rule: Add semicolons always. Reduces bugs from automatic semicolon insertion.

Correct:
```typescript
const user = getUser();
const name = user.name;
return name;
```

Incorrect:
```typescript
const user = getUser()
const name = user.name
```

---

## Equality Checking

Scope: JS/TS
Rule: Use strict equality (===). Avoids implicit type coercion.

Correct:
```typescript
if (value === 0) { }
if (user === null) { }
```

Incorrect:
```typescript
if (value == 0) { }  // matches 0, "0", false, ""
```

---

## Operators

Scope: JS/TS
Rule: Use ?? for defaults. Coalesces only on null/undefined, not falsy values.

Correct:
```typescript
const value = userInput ?? "default";
const port = config.port ?? 8000;
```

Incorrect:
```typescript
const value = userInput || "default";  // fails if userInput is ""
const port = config.port || 8000;  // fails if port is 0
```

---

## String Methods

Scope: JS/TS
Rule: Use slice() instead of substring() or substr(). substr() deprecated, substring() has confusing behavior.

Correct:
```typescript
const text = "Hello World";
const result = text.slice(0, 5);  // "Hello"
const last = text.slice(-5);  // "World"
```

Incorrect:
```typescript
const result = text.substring(0, 5);
const end = text.substr(6);  // deprecated
```

---

## String Formatting

Scope: JS/TS
Rule: Prefer template strings over concatenation. More readable, allows embedded expressions.

Correct:
```typescript
const greeting = `Hello, ${user.name}!`;
const url = `/api/users/${userId}/posts/${postId}`;
```

Incorrect:
```typescript
const greeting = "Hello, " + user.name + "!";
```

---

## Delete Operator

Scope: JS/TS
Rule: Use delete for object properties only. Variables declared with var/let/const cannot be deleted.

Correct:
```typescript
const obj = { name: "John", age: 30 };
delete obj.age;  // removes property
```

Incorrect:
```typescript
let userName = "John";
delete userName;  // returns false, variable remains
```

Note: For arrays, use splice() or filter():
```typescript
const arr = [1, 2, 3];
arr.splice(1, 1);  // removes element
```

---

## Function Arguments

Scope: JS/TS
Rule: Use rest operator instead of arguments object. More consistent and readable.

Correct:
```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((a, b) => a + b, 0);
}
```

Incorrect:
```typescript
function sum() {
  return Array.from(arguments).reduce((a, b) => a + b, 0);
}
```

---

## Array Iteration

Scope: JS/TS
Rule: Prefer for..of for array values. More readable, no index access needed.

Correct:
```typescript
for (const item of items) {
  process(item);
}

for (const [index, item] of items.entries()) {
  console.log(index, item);
}
```

Incorrect:
```typescript
for (let i = 0; i < items.length; i++) {
  process(items[i]);
}
```

Exception: Use for loop when break/continue or index manipulation needed.

---

## Dangerous Features

Scope: JS/TS
Rule: Avoid eval, prototype manipulation, Object.defineProperty. Security risks and maintenance issues.

Incorrect:
```typescript
eval("const x = 1");  // security risk
Array.prototype.myMethod = function() { };  // pollutes global
Object.defineProperty(obj, "prop", { get() { } });  // confusing
```
