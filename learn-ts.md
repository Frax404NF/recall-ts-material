### Catatan Recall Materi TS 24 September 2025

# Types in TS

TypeScript provides static typing for JavaScript. Types help catch errors early and improve code readability.

- **Basic types:**
  - `string`, `number`, `boolean`, `null`, `undefined`, `any`, `void`, `never`
- **Example:**

```typescript
let age: number = 25;
let name: string = "Alice";
let isActive: boolean = true;
```

# Custom types in TS

Custom types allow you to define the structure of objects and data in your application.

- **Type alias:**
  - Use `type` to create a custom type.
- **Interface:**
  - Use `interface` for object shapes (often used for classes or complex objects).

### Example using `type`:
```typescript
type User = {
  id: number;
  name: string;
  email: string;
  isActive: boolean;
};
```

### Example using `interface`:
```typescript
interface Product {
  id: number;
  name: string;
  price: number;
}
```

Custom types make your code safer and easier to maintain.

# Export vs Non-Export in TypeScript

## With `export`
- Types and functions can be imported and reused in other files/modules.
- Promotes modularity and code sharing.

### Example
```typescript
// user.ts
export type User = {
  id: number;
  name: string;
  email: string;
  isActive: boolean;
};

export const createUser = (user: User): User => user;
```

```typescript
// profile.ts
import { User, createUser } from './user';
const admin: User = createUser({
  id: 2,
  name: "Admin",
  email: "admin@example.com",
  isActive: true,
});
```

## Without `export`
- Types and functions are only available in the current file.
- Cannot be accessed from other files.

### Example
```typescript
// index.ts
// ...existing code...
```

## When to Use `export`
- When you want to share code between files (e.g., models, utilities, constants).
- In real-world applications, use `export` for shared logic, types, and helpers.

## When Not to Use `export`
- For code only needed in a single file (e.g., private helpers, local types).


# Nested object types

Nested object types allow you to define complex data structures by including one type inside another. This is useful for modeling real-world entities that have related details grouped together.

## Example
```typescript
type Address = {
  street: string;
  city: string;
  country: string;
};

type Person = {
  name: string;
  age: number;
  isStudent: boolean;
  address: Address; // Nested type
};

const person1: Person = {
  name: "Joe",
  age: 42,
  isStudent: true,
  address: {
    street: "123 Main",
    city: "Anytown",
    country: "USA"
  }
};
```

## Why use nested types?
- Keeps code organized and readable
- Makes it easy to reuse types (e.g., `Address` can be used in multiple places)
- Helps catch errors by enforcing structure

## Best practice
- Define nested types separately for clarity and reusability
- Use optional properties (`?`) if some nested fields may be missing

## Real-world example
A `User` might have a `Profile` type, and a `Profile` might have an `Address` type:
```typescript
type Address = {
  street: string;
  city: string;
  country?: string; // Optional
};

type Profile = {
  bio: string;
  address?: Address; // Optional nested type
};

type User = {
  id: number;
  name: string;
  profile?: Profile;
};
```
This approach makes your code modular and easier to maintain.
