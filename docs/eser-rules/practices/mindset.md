# Coding Mindset

## Self-Documenting Code

Scope: All languages
Rule: Use meaningful variable, class, and function names. Makes code easier to understand and maintain.

Correct:
```typescript
function calculateTotalPrice(items: Item[], taxRate: number): number {
  const subtotal = items.reduce((sum, item) => sum + item.price, 0);
  const tax = subtotal * taxRate;
  return subtotal + tax;
}

class UserAuthenticationService {
  async validateCredentials(username: string, password: string): Promise<boolean> { }
}
```

Incorrect:
```typescript
function calc(arr: Item[], r: number): number {
  const s = arr.reduce((a, b) => a + b.price, 0);  // what is s?
  const t = s * r;  // what is t?
  return s + t;
}

class UAS {  // unclear abbreviation
  async validate(u: string, p: string): Promise<boolean> { }  // u? p?
}
```

---

## Comments

Scope: All languages
Rule: Use comments to explain 'why' and 'how' if code is not self-explanatory. Important for complex logic.

Correct:
```typescript
// Use binary search because dataset can be very large (10M+ items)
// Linear search would be O(n), binary search is O(log n)
function findUser(users: User[], id: string): User | null {
  // Binary search implementation
}

// Cache results for 5 minutes to reduce database load
// Trade-off: slight staleness for better performance
const cache = new Map<string, CachedValue>();
```

Incorrect:
```typescript
// This function finds a user
function findUser(users: User[], id: string): User | null {  // redundant comment
}

const x = 5 * 60 * 1000;  // no explanation of why this specific value
```

Good practices:
- Explain why, not what (code shows what)
- Document trade-offs and decisions
- Explain non-obvious algorithms or optimizations
- Note important constraints or assumptions

---

## Don't Repeat Yourself

Scope: All languages
Rule: Abstract common functionality into reusable modules or functions. Keeps codebase DRY and maintainable.

Correct:
```typescript
function formatUserName(user: User): string {
  return `${user.firstName} ${user.lastName}`;
}

function displayWelcome(user: User) {
  console.log(`Welcome, ${formatUserName(user)}`);
}

function sendEmail(user: User) {
  email.send(`Hello ${formatUserName(user)}`);
}
```

Incorrect:
```typescript
function displayWelcome(user: User) {
  console.log(`Welcome, ${user.firstName} ${user.lastName}`);  // duplicated
}

function sendEmail(user: User) {
  email.send(`Hello ${user.firstName} ${user.lastName}`);  // duplicated
}

function updateProfile(user: User) {
  const name = `${user.firstName} ${user.lastName}`;  // duplicated again
}
```

When to abstract:
- Used 3+ times: definitely abstract
- Used 2 times: consider abstracting if logic is complex
- Used 1 time: keep inline unless it improves clarity
