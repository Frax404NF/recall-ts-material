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

# Array in TS

Arrays in TypeScript are used to store lists of data. You can specify the type of elements an array should contain, which helps catch errors and makes your code safer.

---

## 1. Basic Array Declarations
TypeScript supports two syntaxes for arrays:

- **Type followed by []**
```typescript
let numbers: number[] = [1, 2, 3, 4, 5];
let names: string[] = ["Alice", "Bob", "Charlie"];
let booleans: boolean[] = [true, false, true];
```
- **Generic syntax**
```typescript
let moreNumbers: Array<number> = [10, 20, 30];
let moreNames: Array<string> = ["David", "Eve"];
```

---

## 2. Array of Objects
You can create arrays of objects using interfaces or types:
```typescript
interface Person {
  name: string;
  age: number;
}

let people: Person[] = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 },
  { name: "Bob", age: 22 }
];
```

---

## 3. Mixed Types (Union Types)
Arrays can hold multiple types using union types:
```typescript
let mixedArray: (string | number)[] = [1, "hello", 2, "world"];
let mixedArray2: Array<string | number | boolean> = [1, "text", true, 42];
```

---

## 4. Nested Arrays (Multidimensional)
You can create arrays of arrays:
```typescript
let matrix: number[][] = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

let stringMatrix: string[][] = [
  ["a", "b", "c"],
  ["d", "e", "f"]
];
```

---

## 5. Tuple Arrays (Fixed length and types)
Tuples are arrays with fixed length and types:
```typescript
let coordinates: [number, number] = [10, 20];
let personInfo: [string, number, boolean] = ["Alice", 25, true];

// Array of tuples
let coordinatesList: [number, number][] = [
  [0, 0],
  [10, 20],
  [30, 40]
];
```

---

## 6. Readonly Arrays (Immutable)
Readonly arrays cannot be modified:
```typescript
let readonlyNumbers: readonly number[] = [1, 2, 3];
let readonlyNames: ReadonlyArray<string> = ["Alice", "Bob"];
// readonlyNumbers.push(4); // ❌ Error! Cannot modify
// readonlyNumbers[0] = 10; // ❌ Error! Cannot modify
```

---

## 7. Array Methods with Types
TypeScript checks types when using array methods:
```typescript
let fruits: string[] = ["apple", "banana", "cherry"];
fruits.push("date"); // ✅ OK
// fruits.push(123); // ❌ Error!

let longFruits: string[] = fruits.filter(fruit => fruit.length > 5);
let fruitLengths: number[] = fruits.map(fruit => fruit.length);
let foundFruit: string | undefined = fruits.find(fruit => fruit.startsWith('a'));
```

---

## 8. Optional Array Properties
Arrays can be optional in object types:
```typescript
interface User {
  name: string;
  hobbies?: string[]; // Optional array
}

let user1: User = { name: "Alice" };
let user2: User = { name: "Bob", hobbies: ["reading", "swimming"] };
```

---

## 9. Array Destructuring
You can extract values from arrays easily:
```typescript
let colors: string[] = ["red", "green", "blue"];
let [first, second, ...rest] = colors;
// first: "red", second: "green", rest: ["blue"]
```

---

## 10. Common Array Patterns
- **Empty array with type annotation**
```typescript
let emptyNumbers: number[] = [];
let emptyStrings: string[] = [];
```
- **Array with initial values**
```typescript
let scores: number[] = new Array(5).fill(0); // [0, 0, 0, 0, 0]
```
- **Array from other arrays**
```typescript
let allNumbers: number[] = [...numbers, ...moreNumbers];
```

---

## 11. Array Type Guards
Type guards help check array types at runtime:
```typescript
function isStringArray(arr: any[]): arr is string[] {
  return arr.every(item => typeof item === 'string');
}

let unknownArray: any[] = ["a", "b", "c"];
if (isStringArray(unknownArray)) {
  // TypeScript now knows unknownArray is string[]
  console.log(unknownArray.join(', '));
}
```

---

## Summary
- Arrays can hold any type, but specifying the type makes your code safer
- Use `type[]` or `Array<type>` for type-safe arrays
- Combine arrays with custom types for real-world data structures
- Use tuples, readonly arrays, and type guards for advanced patterns


# TypeScript Literal Types and Union Types

## What are Literal Types?

Literal types represent **exact, specific values** rather than broad categories of values.

### Examples of Literal Types

```typescript
// String literals - only accepts this exact string
let status: "active" = "active";
// status = "inactive"; // ❌ Error! Only "active" allowed

// Number literals - only accepts this exact number
let count: 5 = 5;
// count = 6; // ❌ Error! Only 5 allowed

// Boolean literals - only accepts this exact boolean
let isEnabled: true = true;
// isEnabled = false; // ❌ Error! Only true allowed
```

### Literal vs Non-Literal Types

| Type | Example | What it accepts |
|------|---------|-----------------|
| Non-literal | `string` | Any string value |
| Literal | `"hello"` | Only the string "hello" |
| Non-literal | `number` | Any number value |
| Literal | `42` | Only the number 42 |
| Non-literal | `boolean` | true or false |
| Literal | `true` | Only true |

## What are Union Types?

Union types use the `|` (pipe) operator to combine multiple types. It means "this OR that".

### Basic Union Examples

```typescript
// Can be string OR number
let value: string | number;
value = "hello";  // ✅ OK
value = 42;       // ✅ OK
// value = true;  // ❌ Error! boolean not allowed

// Can be any of these three types
let data: string | number | boolean;
data = "text";    // ✅ OK
data = 123;       // ✅ OK
data = false;     // ✅ OK
```

## The Power Combination: Literal + Union

When you combine literals with unions, you get **precise control** over what values are allowed.

### String Literal Unions

```typescript
// Only these exact strings are allowed
type Status = "loading" | "success" | "error";

let currentStatus: Status = "loading";  // ✅ OK
currentStatus = "success";              // ✅ OK
currentStatus = "error";                // ✅ OK
// currentStatus = "pending";           // ❌ Error! Not in the union
```

### Number Literal Unions

```typescript
// Only these exact numbers are allowed
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;

let roll: DiceRoll = 4;  // ✅ OK
// roll = 7;             // ❌ Error! Only 1-6 allowed
```

### Mixed Literal Unions

```typescript
// Mix different types of literals
type Config = "enabled" | "disabled" | 0 | 1;

let setting: Config = "enabled";  // ✅ OK
setting = 0;                      // ✅ OK  
setting = 1;                      // ✅ OK
// setting = "maybe";             // ❌ Error!
```

## Why Use Literal Types?

### 1. Prevent Typos and Invalid Values

```typescript
// ❌ Without literals - prone to errors
let theme: string = "ligt";  // Typo! But TypeScript allows it

// ✅ With literals - catches errors
let theme: "light" | "dark" = "ligt";  // ❌ TypeScript catches the typo!
```

### 2. Better IntelliSense

When you use literal unions, your IDE will show you exactly what options are available.

### 3. Exhaustive Checking

```typescript
type Direction = "up" | "down" | "left" | "right";

function move(direction: Direction) {
  switch (direction) {
    case "up":
      // Handle up
      break;
    case "down":
      // Handle down  
      break;
    case "left":
      // Handle left
      break;
    case "right":
      // Handle right
      break;
    // TypeScript knows all cases are covered - no default needed!
  }
}
```

## When to Use Each Type

### Use Non-Literal Types For:
- User input (names, descriptions, comments)
- Calculated values (prices, totals, timestamps)
- Data that varies widely
- External API responses (when you don't control the format)

```typescript
interface User {
  name: string;        // Names vary - use non-literal
  email: string;       // Emails vary - use non-literal
  age: number;         // Ages vary - use non-literal
}
```

### Use Literal Union Types For:
- Fixed set of valid options
- Configuration values
- Status/state management
- API endpoints or methods
- Preventing invalid combinations

```typescript
interface ApiRequest {
  method: "GET" | "POST" | "PUT" | "DELETE";    // Fixed HTTP methods
  status: 200 | 201 | 400 | 401 | 500;         // Valid status codes
  environment: "dev" | "staging" | "production"; // Valid environments
}
```

## Type Narrowing with Literals

TypeScript can "narrow" union types based on your code:

```typescript
type Animal = "cat" | "dog" | "bird";

function makeSound(animal: Animal) {
  if (animal === "cat") {
    // TypeScript knows animal is exactly "cat" here
    console.log("Meow!");
  } else if (animal === "dog") {
    // TypeScript knows animal is exactly "dog" here
    console.log("Woof!");
  } else {
    // TypeScript knows animal must be "bird" here
    console.log("Tweet!");
  }
}
```

## Advanced Pattern: Discriminated Unions

Use a common property with literal types to create powerful type-safe patterns:

```typescript
type LoadingState = {
  status: "loading";
  message: string;
};

type SuccessState = {
  status: "success";
  data: any[];
};

type ErrorState = {
  status: "error";
  error: string;
};

type AppState = LoadingState | SuccessState | ErrorState;

function handleState(state: AppState) {
  switch (state.status) {
    case "loading":
      // TypeScript knows this is LoadingState
      console.log(state.message);
      break;
    case "success":
      // TypeScript knows this is SuccessState
      console.log(`Loaded ${state.data.length} items`);
      break;
    case "error":
      // TypeScript knows this is ErrorState
      console.log(`Error: ${state.error}`);
      break;
  }
}
```

## Key Takeaways

1. **Literal types** = exact specific values
2. **Union types** = combine types with `|` (OR operator)  
3. **Literal unions** = combine specific values for precise control
4. Use **non-literals** for flexible data
5. Use **literal unions** for fixed options and configuration
6. TypeScript provides **type narrowing** and **exhaustive checking**
7. **Discriminated unions** are powerful for state management

## Common Patterns

```typescript
// HTTP methods
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE" | "PATCH";

// Response status
type ResponseStatus = "success" | "error" | "loading";

// User roles  
type UserRole = "admin" | "user" | "guest";

// Themes
type Theme = "light" | "dark" | "auto";

// File types
type FileType = "pdf" | "doc" | "txt" | "img";
```

This combination of literal and union types is one of TypeScript's most powerful features for creating type-safe, maintainable code!