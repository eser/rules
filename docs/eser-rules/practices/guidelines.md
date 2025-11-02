# Coding Guidelines

## Input Validation

Scope: All languages
Rule: Validate input data. Ensures robustness and prevents bugs or security vulnerabilities.

Correct:
```typescript
function createUser(email: string, age: number): User {
  if (!email.includes("@")) throw new Error("Invalid email");
  if (age < 0 || age > 150) throw new Error("Invalid age");
  return { email, age };
}
```

Incorrect:
```typescript
function createUser(email: string, age: number): User {
  return { email, age };  // no validation
}
```

---

## Error Handling

Scope: All languages
Rule: Handle all possible error cases. Ensures graceful recovery and better user experience.

Correct:
```typescript
async function fetchUser(id: string): Promise<User | null> {
  try {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) return null;
    return await response.json();
  } catch (error) {
    console.error("Failed to fetch user", error);
    return null;
  }
}
```

Incorrect:
```typescript
async function fetchUser(id: string): Promise<User> {
  const response = await fetch(`/api/users/${id}`);  // unhandled
  return await response.json();
}
```

---

## Error Objects

Scope: All languages
Rule: Use proper error objects. Include context via properties/cause. Avoid string concatenation in messages.

Correct:
```typescript
throw new Error("Failed to process payment", {
  cause: { userId, amount, reason: "Insufficient funds" }
});

try {
  processPayment(data);
} catch (error) {
  throw new Error("Payment processing failed", { cause: error });
}
```

Incorrect:
```typescript
throw new Error("Failed for user " + userId + " amount " + amount);
throw "Payment failed";  // not an Error object
```

---

## Specific Error Types

Scope: All languages
Rule: Throw specific error types, not generic errors. Provides better context.

Correct:
```typescript
class ValidationError extends Error {
  constructor(message: string, public field: string) {
    super(message);
    this.name = "ValidationError";
  }
}

throw new ValidationError("Invalid email", "email");
```

Incorrect:
```typescript
throw new Error("Something went wrong");  // too generic
```

---

## Result Objects

Scope: All languages
Rule: Consider result objects instead of throwing errors. More predictable.

Correct:
```typescript
type Result<T, E> = { ok: true; value: T } | { ok: false; error: E };

function parseData(input: string): Result<Data, string> {
  if (!input) return { ok: false, error: "Empty input" };
  try {
    return { ok: true, value: JSON.parse(input) };
  } catch {
    return { ok: false, error: "Invalid JSON" };
  }
}

const result = parseData(input);
if (result.ok) {
  process(result.value);
}
```

---

## Ignored Errors

Scope: All languages
Rule: Never ignore returned errors. Handle appropriately.

Correct:
```typescript
try {
  await saveToDatabase(data);
} catch (error) {
  console.error("Failed to save", error);
  throw new Error("Database operation failed", { cause: error });
}
```

Incorrect:
```typescript
try {
  await saveToDatabase(data);
} catch (error) {
  // ignored
}
```

---

## Assertions

Scope: All languages
Rule: Use assertions to verify pre/post-conditions and invariants. Documents assumptions.

Correct:
```typescript
function divide(a: number, b: number): number {
  console.assert(b !== 0, "Divisor must not be zero");
  console.assert(Number.isFinite(a), "Dividend must be finite");
  return a / b;
}
```

---

## Logging

Scope: All languages
Rule: Use logging for tracing and debugging. Helps understand program flow.

Correct:
```typescript
function processOrder(order: Order) {
  console.log("Processing order", { orderId: order.id });
  try {
    const result = validateOrder(order);
    console.log("Order validated", { orderId: order.id });
    return result;
  } catch (error) {
    console.error("Validation failed", { orderId: order.id, error });
    throw error;
  }
}
```

---

## Circular Dependencies

Scope: All languages
Rule: Avoid circular dependencies. Leads to unexpected behavior.

Incorrect:
```typescript
// file-a.ts
import { funcB } from "./file-b.ts";
export function funcA() { funcB(); }

// file-b.ts
import { funcA } from "./file-a.ts";  // circular
export function funcB() { funcA(); }
```

---

## Magic Values

Scope: All languages
Rule: Avoid magic numbers or strings. Use named constants.

Correct:
```typescript
const MAX_RETRIES = 3;
const API_TIMEOUT_MS = 5000;

if (retries >= MAX_RETRIES) { }
setTimeout(callback, API_TIMEOUT_MS);
```

Incorrect:
```typescript
if (retries >= 3) { }  // what is 3?
setTimeout(callback, 5000);  // what is 5000?
```
