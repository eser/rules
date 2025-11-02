# JavaScript/TypeScript Delete Operator

## Delete Usage

Scope: JS/TS Rule: Use delete to remove object properties only. Variables
declared with var, let, const cannot be deleted (delete returns false).

Correct:

```typescript
const obj = { name: "John", age: 30 };
delete obj.age; // removes property, returns true
console.log(obj); // { name: "John" }

const map = { key1: "value1", key2: "value2" };
delete map.key1; // removes property
```

Incorrect:

```typescript
let userName = "John";
delete userName; // returns false, variable remains

const config = { port: 8000 };
delete config; // returns false, variable remains

var data = [1, 2, 3];
delete data; // returns false, variable remains
```

Note: For arrays, use splice() or filter() instead of delete:

```typescript
const arr = [1, 2, 3];
arr.splice(1, 1); // removes element at index 1
// or
const filtered = arr.filter((_, i) => i !== 1);
```
