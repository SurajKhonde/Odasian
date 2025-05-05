# Initial Setup
Install Typescript as a development dependency:
```bash
npm install typescript --save-dev
```
## theory of typescript
Learning Type Script in node.Js project
The **TypeScript** language is a typed **superset** of JavaScript, which is compiled to plain JavaScript in the flavor of your choosing.
This makes programs written in TypeScript highly portable as they can run  
on almost any machine — in web browsers, on web servers, and even in native applications on operating  
systems that expose a JavaScript API, such as WinJS.  
![[image.png]]
**Compile or Transpile?**

The term **transpiling** has been around since the last century, but there is some confusion about its meaning. In particular, there has been some confusion between the terms compilation and **transpilation**. Compilation describes the process of taking source code written in one language and converting it into another language.

**Transpilation** is a specific kind of compilation and describes the process of taking source **code written in one language and transforming it into another language with a similar level of abstraction.** So, you might compile  
a high-level language into an assembly language, but you would  
**transpile TypeScript to JavaScript as they are similarly abstracted.**

JavaScript can even be used to write native applications on operating systems such as Windows.

**TypeScript** is a language, a compiler, and a language service.  
• You can paste existing JavaScript into your TypeScript program.  
• Compiling from TypeScript to JavaScript is known specifically as transpiling.  
•  
**TypeScript** is not the only alternative way of writing JavaScript, but it has gained incredible traction in its first five years.
TypeScript is a superset of JavaScript.That means that the TypeScript language includes the entire JavaScript language plus a collection of useful additional features.
The TypeScript compiler is typically updated with new JavaScript features early in their specification.  
Most of the features are available before browsers support them.  
TypeScript variables must follow the JavaScript naming rules. The identifier used to name a variable must satisfy the following conditions.
**All JavaScript is valid TypeScript**
**Scope in TypeScript:**

```typescript
function greet() {
  let firstName = "Alice";

  if (true) {
    let firstName = "Bob"; // Shadowing the outer variable
    console.log(firstName); // Bob
  }

  console.log(firstName); // Alice
}
```
Types  
TypeScript is optionally statically typed; this means that types are checked automatically to prevent accidental assignments of invalid values. It is possible to opt out of this by declaring dynamic variables.  
Static type checking reduces errors caused by accidental misuse of types  
**Type Annotations**
![[image 1.png]]
`const name: string = 'Steve';`
TypeScript provides a **rich type system** that allows for precise type annotations. Here’s a breakdown of the different type options:
**1. Primitive Types**
```typescript
let age: number = 25;
let name: string = "Alice";
let isAdmin: boolean = true;
```
2. Array Types
```typescript
let numbers: number[] = [1, 2, 3]; // Array of numbers
let names: string[] = ["Alice", "Bob"];
```
3. Function Signature Types
```typescript
let greet: (name: string) => string;
greet = (name) => `Hello, ${name}`;
```
**4. Type Alias**
A **type alias** allows you to define a reusable type:

```typescript
type User = {
  id: number;
  name: string;
};
let user: User = { id: 1, name: "Alice" };
```
**5. Union Types (Permissive)**
A **union type** allows multiple possible types:
```typescript
let id: string | number;
id = 101;  // Valid
id = "ABC"; // Valid
// id = true; // ❌ Error
```
**6. Literal Types (Restrictive)**
```typescript
type Status = "success" | "error" | "loading";
let requestStatus: Status = "success"; // ✅ Allowed
// requestStatus = "failed"; // ❌ Error
```
7. The `any` Type (Dynamic, Opt-Out of Type Checking)
Using `any` disables type checking:
```typescript
let data: any = 42;
data = "Now it's a string"; // No error
```
 **Downside:** `any` removes TypeScript’s safety, so use it sparingly.
8. Interfaces and Class Names
```typescript
interface Person {
  name: string;
  age: number;
}

class Employee {
  constructor(public name: string, public age: number) {}
}

let emp: Employee = new Employee("Alice", 30);
```
**enumeration**
```typescript
enum Status {
  Pending,   // 0
  InProgress, // 1
  Completed   // 2
}

let taskStatus: Status = Status.InProgress;
console.log(taskStatus); // Output: 1
//🔹 Custom Values: You can manually assign values.

enum Status {
  Pending = 10,
  InProgress = 20,
  Completed = 30
}

console.log(Status.Completed); // 30
//String Enums
enum Role {
  Admin = "ADMIN",
  User = "USER",
  Guest = "GUEST"
}

let userRole: Role = Role.User;
console.log(userRole); // Output: "USER"
//Heterogeneous Enums (Mixed Values)
enum Mixed {
  Yes = "YES",
  No = 0
}

```
**Using Enums in Functions**
```typescript
function getStatusMessage(status: Status): string {
  switch (status) {
    case Status.Pending:
      return "Task is pending...";
    case Status.InProgress:
      return "Task is in progress...";
    case Status.Completed:
      return "Task is completed!";
    default:
      return "Unknown status";
  }
}

console.log(getStatusMessage(Status.InProgress)); 
// Output: "Task is in progress..."
```
5. Enum Reverse Mapping
In numeric enums, you can **access keys from values**.
```typescript
enum Color {
  Red = 1,
  Green,
  Blue
}

console.log(Color[1]); // "Red"
console.log(Color.Red); // 1
// This does not work with string enums
// because strings don’t have reverse mapping.
```
6. `const enum` for Performance Optimization
When using `const enum`, TypeScript **removes it from the compiled JavaScript**, making the code more optimized.
```typescript
const enum Direction {
  Up,
  Down
}
console.log(Direction.Up); // Directly replaced with 0 at runtime
```
**Arrays in TypeScript**
In TypeScript, arrays allow you to store multiple values of the **same type** (or a mix of types using union types). You can define arrays using **two methods**:
1. **Type followed by** `**[]**`
2. **Using** `**Array<type>**` **generic syntax**
```typescript
let numbers: number[] = [1, 2, 3, 4, 5]; 
let names: string[] = ["Alice", "Bob", "Charlie"];
Or using the generic type syntax:
let numbers: Array<number> = [1, 2, 3, 4, 5];
```
**2. Mixed-Type Arrays**
You can store multiple **different types** using **union types**:
```typescript
let mixed: (string | number)[] = [1, "hello", 2, "world"];
```
**3. Readonly Arrays (**`**readonly**`**)**
```typescript
const colors: readonly string[] = ["red", "green", "blue"];
// colors.push("yellow"); ❌ Error: Cannot modify a readonly array
```
**4. Tuple (Fixed-Length Arrays)**
```typescript
let person: [string, number] = ["Alice", 30];
//You can add optional or rest elements:
let person: [string, number, boolean?] = ["Bob", 25]; // Optional boolean
```
**6. Common Array Methods**
```typescript
let fruits: string[] = ["Apple", "Banana", "Cherry"];

// Push & Pop
fruits.push("Orange"); // ["Apple", "Banana", "Cherry", "Orange"]
fruits.pop(); // ["Apple", "Banana", "Cherry"]

// Map
let upperCaseFruits = fruits.map(fruit => fruit.toUpperCase());
console.log(upperCaseFruits); // ["APPLE", "BANANA", "CHERRY"]

// Filter
let filteredFruits = fruits.filter(fruit => fruit !== "Banana");
console.log(filteredFruits); // ["Apple", "Cherry"]

// Reduce
let numbers: number[] = [1, 2, 3, 4];
let sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```
### **When to Use Each Type Guard?**

|   |   |
|---|---|
|Type Guard|Use Case|
|`typeof`|For **primitives** (`string`, `number`, `boolean`)|
|`instanceof`|For **classes and constructors**|
|`in`|For **checking object properties**|
|Custom Guard (`is`)|For **complex object validation**|
|Discriminated Unions|For **handling API responses or multiple types**|

```typescript
class Dog {
  bark() {
    console.log("Woof!");
  }
}

class Cat {
  meow() {
    console.log("Meow!");
  }
}

function makeSound(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark(); // ✅ Safe to call
  } else {
    animal.meow(); // ✅ Safe to call
  }
}
```
**Destructuring in JavaScript & TypeScript** 🚀
Destructuring allows you to **extract values from objects and arrays** in a **clean and readable** way. It's useful in function parameters, assignments, loops, and more.
```typescript
const user = { name: "Alice", age: 25, country: "USA" };
const { name, age } = user;
console.log(name, age); // Alice 25

✅ Renaming Variables
const { name: userName, age: userAge } = user;
console.log(userName, userAge); // Alice 25
✅ Default Values
const { name, gender = "Not specified" } = user;
console.log(gender); // Not specified
```
**Function Overloads in TypeScript 🚀**
**Function Overloads** allow you to define **multiple function signatures** for a single function. This is useful when a function behaves **differently based on input types**.

**📌 1. Why Use Function Overloads?**
######  When Not to Use Overloads
- **Use Union Types**: `string | number`
- **Use Optional Parameters**: `param?: string`
- **Use Default Values**: `param = "default"`
- **Use Rest Parameters**: `(...args: number[])`
 **Only use overloads if these options don’t work.**
```typescript
function add(a: number, b: number): number;
function add(a: string, b: string): string;

// Implementation Signature (Hidden)
function add(a: number | string, b: number | string): number | string {
  if (typeof a === "string" && typeof b === "string") {
    return a + b; // String concatenation
  }
  if (typeof a === "number" && typeof b === "number") {
    return a + b; // Number addition
  }
  throw new Error("Invalid arguments");
}

console.log(add(10, 20)); // 30
console.log(add("Hello, ", "World!")); // Hello, World!
```
**Overload Signatures** (`function add(a: number, b: number): number;`)
**Single Implementation** (`function add(a: number | string, b: number | string)`)
**Prevents invalid calls** like `add(10, "test")`.
**Arrow Functions**
```typescript
const shortAddNumbers = (a: number, b: number) => a + b;
const mediumAddNumbers = (a: number, b: number) => {
 return a + b;
}
const longAddNumbers = function (a: number, b: number) {
 return a + b;
}
```

**Interfaces in TypeScript**

In TypeScript, an **interface** defines the structure of an object, specifying what properties and methods it should have. It helps ensure type safety and better code organization.

```typescript
interface User {
  name: string;
  age: number;
}

let user: User = {
  name: "Alice",
  age: 30
};

// Error: Missing 'age' property
// let user2: User = { name: "Bob" };
```

**2. Optional and Readonly Properties**

- **Optional (**`**?**`**)**: Some properties may not always be present.

- **Readonly (**`**readonly**`**)**: Prevents modification after initialization.

```typescript
interface Car {
  make: string;
  model: string;
  year?: number;  // Optional property
  readonly vin: string;  // Cannot be changed
}

let myCar: Car = {
  make: "Toyota",
  model: "Corolla",
  vin: "12345ABC"
};

// myCar.vin = "67890XYZ";  // Error: Cannot assign to 'vin' because it is a read-only property
```

1️⃣ Creating a Basic Class

```typescript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

// Creating an instance
const person1 = new Person("Alice", 25);
person1.greet();  // Output: Hello, my name is Alice and I am 25 years old.
```

2️⃣ Class Inheritance (Extending Classes)

Use the `extends` keyword to create a **subclass** (child class) that inherits from a parent class.

```typescript
class Employee extends Person {
  constructor(name, age, jobTitle) {
    super(name, age);  // Calls the constructor of the parent class (Person)
    this.jobTitle = jobTitle;
  }

  work() {
    console.log(`${this.name} is working as a ${this.jobTitle}.`);
  }
}

const emp1 = new Employee("Bob", 30, "Software Developer");
emp1.greet();  // Inherited method
emp1.work();   // Output: Bob is working as a Software Developer.
```

3️⃣ Getters and Setters

- **Getters (**`**get**`**)** allow you to access properties in a controlled way.

- **Setters (**`**set**`**)** allow you to modify properties with additional logic.

```typescript
class Product {
  constructor(name, price) {
    this.name = name;
    this._price = price;  // Using underscore to indicate private variable
  }

  get price() {
    return `$${this._price.toFixed(2)}`; // Formatting price
  }

  set price(newPrice) {
    if (newPrice > 0) {
      this._price = newPrice;
    } else {
      console.log("Price must be positive!");
    }
  }
}

const item = new Product("Laptop", 999.99);
console.log(item.price);  // Output: $999.99
item.price = 1200; 
console.log(item.price);  // Output: $1200.00
```

**4️⃣ Static Methods and Properties**

```typescript
class MathHelper {
  static PI = 3.14159;

  static square(number) {
    return number * number;
  }
}

console.log(MathHelper.PI);  // Output: 3.14159
console.log(MathHelper.square(5));  // Output: 25
```

**Code Organization**

It is not the language that makes programs appear simple. It is the programmer that makes the language appear simple!

✅ **Using Modules (Recommended)**

With modules, we use `**import**` **and** `**export**` to organize code in separate files.

**Step 1: Create a Module (**`**mathOperations.ts**`**)**

```typescript
// mathOperations.ts (Module File)
export function add(a: number, b: number): number {
  return a + b;
}

export function subtract(a: number, b: number): number {
  return a - b;
}
```

Step 2: Import & Use the Module (`app.ts`)

```typescript
// app.ts (Main File)
import { add, subtract } from "./mathOperations";

console.log(add(10, 5)); // Output: 15
console.log(subtract(10, 5)); // Output: 5
```

**🔥 Why Prefer Modules?**

|   |   |   |
|---|---|---|
|Feature|Namespaces (❌)|Modules (✅)|
|**Scope Pollution**|Adds identifiers to the global scope|Fully isolated scope|
|**Scalability**|Harder to manage in large projects|Works well with large applications|
|**Dependency Management**|No built-in support|Supports `import/export` for clean dependencies|
|**Tree-Shaking**|Not supported|Allows unused code elimination|
|**Lazy Loading**|Not possible|Can load modules on demand|

1️⃣ **Re-Exporting Specific Exports**

```typescript
export function add(a: number, b: number): number {
  return a + b;
}

export function subtract(a: number, b: number): number {
  return a - b;
}
//File: index.ts (Re-exporting)
export { add, subtract } from "./mathOperations";
File: app.ts (Using the Re-exported Module)
import { add, subtract } from "./index";

console.log(add(10, 5));  // Output: 15
console.log(subtract(10, 5));  // Output: 5
```

3️⃣ Re-Exporting an Entire Module

You can re-export **all exports** from another module using `export * from`.

Re-exporting an Entire Module

```typescript
 //mathOperations.ts
export function divide(a: number, b: number): number {
  return a / b;
}

export function modulus(a: number, b: number): number {
  return a % b;
}
// index.ts (Re-exporting Entire Module)
export * from "./mathOperations";

File: app.ts (Using Re-exported Functions)
import { divide, modulus } from "./index";
console.log(divide(10, 2));  // Output: 5
console.log(modulus(10, 3)); // Output: 1
```

# TypeScript

### Initial Setup

Install Typescript as a development dependency:
                                          

```bash
npm install typescript --save-dev
```

Install the necessary type definitions for Node.js and Express

```bash
npm install @types/node --save-dev
npm install @types/express --save-dev
```

**Set Up TypeScript Configuration (`tsconfig.json`)**

**npx tsc --init**

```bash
{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "moduleResolution": "node",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "outDir": "./dist", // this will take care convert ts to js 
    "rootDir": "./src",
    "types": ["node", "express"],
    "allowJs": true,   
    "checkJs": true 
  },
  "include": ["src/**/*.ts", "src/**/*.js"], // It Allows .js and .ts 
  "exclude": ["node_modules"]
}
```

**package.json(TypeScript)**

```json
{
  "name": "onestopapi",
  "version": "1.0.0",
  "main": "app.ts",
  "scripts": {
    "dev": "nodemon src/app.ts",  //npm run dev for compile the ts to js 
    "build": "tsc",
    "start": "node dist/app.js"  // for start the project
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "",
  "devDependencies": {
    "@types/cors": "^2.8.17",
    "@types/crypto-js": "^4.2.2",
    "@types/dotenv": "^6.1.1",
    "@types/express": "^5.0.0",
    "@types/jsonwebtoken": "^9.0.7",
    "@types/mysql": "^2.15.26",
    "@types/node": "^22.10.1",
    "ts-node": "^10.9.2",
    "typescript": "^5.7.2"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.4.7",
    "express": "^4.21.1",
    "jsonwebtoken": "^9.0.2",
    "mysql2": "^3.11.5",
    "nodemon": "^3.1.7"
  }
}
```

In TypeScript, the `@types/` namespace is used to manage type definitions for JavaScript libraries that do not include TypeScript typings by default. Libraries such as `express`, `cors`, and others are typically written in JavaScript, and TypeScript needs a separate type definition file to understand the types and help with type-checking, autocompletion, and other TypeScript features.

sample code 

```tsx
import express, { Request, Response } from 'express';
import * as dotenv from 'dotenv';
import init from "./config/db"
import cors from 'cors';
dotenv.config();
const app = express();
const port=3000 
app.use(cors());
app.use(function (req, res, next) {
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, OPTIONS, PUT, PATCH, DELETE");
  res.setHeader("Access-Control-Allow-Headers", "*");
  res.setHeader("Access-Control-Allow-Credentials", "true");
  next();
});
app.get('/', (req: Request, res: Response): void => {
  res.send('Hello World!');
});
app.use(express.json());
init()
  .then(() => {
    console.log('Database initialized successfully.');
    app.listen(port, (): void => {
      console.log(`Server running on http://localhost:${port}`);
    });
  })
  .catch((err) => {
    console.error('Error initializing database:', err);
  })
```

```tsx
import { Request, Response } from 'express';
import { isUserExist } from '../../utils/UtilityRoom';
import jwt from 'jsonwebtoken';

interface RegisterRequestBody {
  email: string;
  password: string;
  user_name: string;
  name: string;
  role: string;
}
export const registerUser = async (req: Request<{}, {}, RegisterRequestBody>, res: Response): Promise<void> => {
    try {
        const { email, password, user_name, name, role } = req.body;
        const userExistInDatabase = await isUserExist(email, user_name);
        if (userExistInDatabase) {
            res.status(400).json({ message: 'User already exists' });
            return;
        }
        const token = jwt.sign({ email, user_name, role }, 'yourSecretKey', { expiresIn: '1h' });
        res.status(201).json({
            message: 'User registered successfully',
            token,
        });

    } catch (error: any) {
        console.error('Error during user registration:', error.message);
        res.status(500).json({ message: 'Internal server error' });
    }
};
```

1. `req: Request<{}, {}, RegisterRequestBody>`

The `Request` type is a generic type provided by Express that allows us to specify the types of data for various parts of the request:

   The `Request<T1, T2, T3, T4>` type is a generic type from Express.

| Type Parameter | Meaning | Example |
| --- | --- | --- |
| `T1` (ParamsDictionary) | Route parameters | `/user/:id` → `{ id: "123" }` |
| `T2` (ResBody) | Expected response body | `{ success: true, message: "User created" }` |
| `T3` (ReqBody) | Expected request body | `{ email: "test@example.com", password: "12345" }` |
| `T4` (ReqQuery) | Query parameters | `/users?name=John` → `{ name: "John" }` |

```tsx
Request<ParamsDictionary, ResBody, ReqBody, ReqQuery>
```

1️⃣ `T1`: **ParamsDictionary** (Route Parameters)

```tsx
import { Request, Response } from "express";

app.get("/users/:id", (req: Request<{ id: string }>, res: Response) => {
  const userId = req.params.id; // TypeScript knows `id` is a string
  res.json({ message: `User ID is ${userId}` });
});
```

2️⃣ `T2`: ResBody (Expected Response Body)

```tsx
type UserResponse = { success: boolean; message: string };

app.get("/check", (req: Request, res: Response<UserResponse>) => {
  res.json({ success: true, message: "Server is running" }); // TypeScript ensures correct response structure
});
✅ TypeScript enforces that res.json() must match UserResponse.
```

**🚀 Do You Always Need `T2 (ResBody)` in `Request<>`?**

👉 **No, in most cases, you can ignore `T2` in `Request<>`.**

Since `res` is used separately from `req`, specifying `ResponseBody` inside `Request<>` is usually **optional** unless you're passing `req` to a function that needs it.

3️⃣ `T3`: **ReqBody (Request Body)**

```tsx
type LoginUserBody = {
  email: string;
  password: string;
};

app.post("/login", (req: Request<{}, {}, LoginUserBody>, res: Response) => {
  const { email, password } = req.body; // TypeScript knows email and password exist
  res.json({ message: `Login attempt for ${email}` });
});
```

- `{}` (the first `{}`): This represents the type for route parameters. In Express, route parameters are part of the URL (e.g., `/user/:id` where `:id` is a parameter). Since there are no route parameters in this case (the function doesn’t deal with URL parameters), we use an empty object `{}` to signify that there are no parameters.
- `{}` (the third `{}`): This represents the type for query parameters. Query parameters are the key-value pairs in the URL (e.g., `/user?id=1`). Again, since no query parameters are used in this function, we specify an empty object `{}`.
- `RegisterRequestBody` (the Forth part): This represents the request body. The request body is where the data sent by the client is located. In this case, we use the `RegisterRequestBody` interface to define the expected structure of the body, which includes `email`, `password`, `user_name`, `name`, and `role`. So, `req.body` will be of type `RegisterRequestBody`.

3. `: Promise<void>`

The function is an **asynchronous function**, indicated by the `Promise<void>` return type.

- **`Promise`**: This indicates that the function is asynchronous and will return a promise.
- **`void`**: This means the function does not return any specific value. In the context of Express, you generally don't need to return a value from your route handler — instead, you handle the response with `res.send()`, `res.json()`, etc.
- So, `Promise<void>` indicates that the function does not return anything (i.e., it doesn't return any data back to the caller), but it does perform asynchronous operations (such as interacting with a database or generating a token), which is why it returns a `Promise`.

```tsx
import { Request, Response } from "express";

type UserParams = { id: string };
type ResponseBody = { success: boolean; data?: any; message: string };
type RequestBody = { name: string; age: number };
type QueryParams = { admin?: string };

app.put(
  "/users/:id",
  (req: Request<UserParams, ResponseBody, RequestBody, QueryParams>, res: Response<ResponseBody>) => {
    const userId = req.params.id; // TypeScript enforces id is a string
    const { name, age } = req.body; // TypeScript enforces name is string, age is number
    const isAdmin = req.query.admin === "true"; // Query params are optional

    res.json({ success: true, data: { userId, name, age, isAdmin }, message: "User updated" });
  }
);

```

## The primitives: `string`, `number`, and `boolean`

JavaScript has three very commonly used [primitives](https://developer.mozilla.org/en-US/docs/Glossary/Primitive): `string`, `number`, and `boolean`. Each has a corresponding type in TypeScript. As you might expect, these are the same names you’d see if you used the JavaScript `typeof` operator on a value of those types:

- `string` represents string values like `"Hello, world"`
- `number` is for numbers like `42`. JavaScript does not have a special runtime value for integers, so there’s no equivalent to `int` or `float` - everything is simply `number`
- `boolean` is for the two values `true` and `false`

## Arrays

To specify the type of an array like `[1, 2, 3]`, you can use the syntax `number[]`; this syntax works for any type (e.g. `string[]` is an array of strings, and so on). You may also see this written as `Array<number>`, which means the same thing. We’ll learn more about the syntax `T<U>` when we cover *generics*.

TypeScript also has a special type, `any`, that you can use whenever you don’t want a particular value to cause typechecking errors.

When a value is of type `any`, you can access any properties of it (which will in turn be of type `any`), call it like a function, assign it to (or from) a value of any type, or pretty much anything else that’s syntactically legal:

```tsx
let obj: any = { x: 0 };
// None of the following lines of code will throw compiler errors.
// Using `any` disables all further type checking, and it is assumed
// you know the environment better than TypeScript.
obj.foo();
obj();
obj.bar = 100;
obj = "hello";
const n: number = obj;
```

The `any` type is useful when you don’t want to write out a long type just to convince TypeScript that a particular line of code is okay.

### `noImplicitAny`

When you don’t specify a type, and TypeScript can’t infer it from context, the compiler will typically default to `any`.

You usually want to avoid this, though, because `any` isn’t type-checked. Use the compiler flag `noImplicitAny` to flag any implicit `any` as an error.

**Type Annotations on Variables**

When you declare a variable using `const`, `var`, or `let`, you can optionally add a type annotation to explicitly specify the type of the variable:

```tsx
let myName: string = "Alice";
//No type annotation needed -- 'myName' inferred as type 'string'
let myName = "Alice";
```

For the most part you don’t need to explicitly learn the rules of inference. If you’re starting out, try using fewer type annotations than you think - you might be surprised how few you need for **TypeScript** to fully understand what’s going on.

**Functions**

Functions are the primary means of passing data around in JavaScript. TypeScript allows you to specify the types of both the input and output values of functions.

**Parameter Type Annotations**

When you declare a function, you can add type annotations after each parameter to declare what types of parameters the function accepts. Parameter type annotations go after the parameter name:

```tsx
// Parameter type annotation
function greet(name: string) {
  console.log("Hello, " + name.toUpperCase() + "!!");
}
// Would be a runtime error if executed!
greet(42);
Argument of type 'number' is not assignable to parameter of type 'string'.
```

**Return Type Annotations**

You can also add return type annotations. Return type annotations appear after the parameter list:

```tsx
function getFavoriteNumber(): number {
  return 26;
}
```

Much like variable type annotations, you usually don’t need a return type annotation because TypeScript will infer the function’s return type based on its `return` statements. The type annotation in the above example doesn’t change anything. Some codebases will explicitly specify a return type for documentation purposes, to prevent accidental changes, or just for personal preference.

**Functions Which Return Promises**

If you want to annotate the return type of a function which returns a promise, you should use the `Promise` type:

```tsx
async function getFavoriteNumber(): Promise<number> {
  return 26;
}
```

**Anonymous Functions**

Anonymous functions are a little bit different from function  declarations. When a function appears in a place where TypeScript can determine how  it’s going to be called, the parameters of that function are  automatically given types.

```tsx
const names = ["Alice", "Bob", "Eve"];
 
// Contextual typing for function - parameter s inferred to have type string
names.forEach(function (s) {
  console.log(s.toUpperCase());
});
 
// Contextual typing also applies to arrow functions
names.forEach((s) => {
  console.log(s.toUpperCase());
});
```

Even though the parameter `s` didn’t have a type annotation, TypeScript used the types of the `forEach` function, along with the inferred type of the array, to determine the type `s` will have.

This process is called **contextual typing** because the *context* that the function occurred within informs what type it should have.

Similar to the inference rules, you don’t need to explicitly learn how this happens, but understanding that it *does* happen can help you notice when type annotations aren’t needed.

## Object Types

Apart from primitives, the most common sort of type you’ll encounter is an *object type*. This refers to any JavaScript value with properties, which is almost all of them! To define an object type, we simply list its properties and their types.

```tsx
// The parameter's type annotation is an object type
function printCoord(pt: { x: number; y: number }) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });
```

Here, we annotated the parameter with a type with two properties - `x` and `y` - which are both of type `number`. You can use `,` or `;` to separate the properties, and the last separator is optional either way.

The type part of each property is also optional. If you don’t specify a type, it will be assumed to be `any`

**Optional Properties**

Object types can also specify that some or all of their properties are *optional*. To do this, add a `?` after the property name

```tsx
function printName(obj: { first: string; last?: string }) {
  // ...
}
// Both OK
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });

function printName(obj: { first: string; last?: string }) {
  // Error - might crash if 'obj.last' wasn't provided!
  console.log(obj.last.toUpperCase());
'obj.last' is possibly 'undefined'.

  if (obj.last !== undefined) {
    // OK
    console.log(obj.last.toUpperCase());
  }
 
  // A safe alternative using modern JavaScript syntax:
  console.log(obj.last?.toUpperCase());
}
```

**Union Types**

TypeScript’s type system allows you to build new types out of existing ones using a large variety of operators. Now that we know how to write a few types, it’s time to start *combining* them in interesting ways.

**Defining a Union Type**

The first way to combine types you might see is a *union* type. A union type is a type formed from two or more other types, representing values that may be *any one* of those types. We refer to each of these types as the union’s *members*.

```tsx
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
// OK
printId(101);
// OK
printId("202");
// Error
printId({ myID: 22342 });
Argument of type '{ myID: number; }' is not assignable to parameter of type 'string | number'.
```

```tsx
function printTextOrNumberOrBool(
  textOrNumberOrBool:
    | string
    | number
    | boolean
) {
  console.log(textOrNumberOrBool);
}
```

**Working with Union Types**

It’s easy to *provide* a value matching a union type - simply provide a type matching any of the union’s members. If you *have* a value of a union type, how do you work with it?

TypeScript will only allow an operation if it is valid for *every* member of the union. For example, if you have the union `string | number`, you can’t use methods that are only available on `string`:

```tsx
function printId(id: number | string) { // 
  console.log(id.toUpperCase());
Property 'toUpperCase' does not exist on type 'string | number'.
  Property 'toUpperCase' does not exist on type 'number'.

}
```

The solution is to *narrow* the union with code, the same as you would in JavaScript without type annotations. *Narrowing* occurs when TypeScript can deduce a more specific type for a value based on the structure of the code.

For example, TypeScript knows that only a `string` value will have a `typeof` value `"string"`:

```tsx
function printId(id: number | string) {
  if (typeof id === "string") {
    // In this branch, id is of type 'string'
    console.log(id.toUpperCase());
  } else {
    // Here, id is of type 'number'
    console.log(id);
  }
}

function welcomePeople(x: string[] | string) {
  if (Array.isArray(x)) {
    // Here: 'x' is 'string[]'
    console.log("Hello, " + x.join(" and "));
  } else {
    // Here: 'x' is 'string'
    console.log("Welcome lone traveler " + x);
  }
}
```

**Interfaces**

An *interface declaration* is another way to name an object type:

```tsx
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

Just like when we used a type alias above, the example works just as if we had used an anonymous object type. TypeScript is only concerned with the *structure* of the value we passed to `printCoord` - it only cares that it has the expected properties. Being concerned only with the structure and capabilities of types is why we call TypeScript a *structurally typed* type system.
![[image 2.png]]
![[image 1 1.png]]

**Literal Types**

In addition to the general types `string` and `number`, we can refer to *specific* strings and numbers in type positions.

One way to think about this is to consider how JavaScript comes with different ways to declare a variable. Both `var` and `let` allow for changing what is held inside the variable, and `const` does not. This is reflected in how TypeScript creates types for literals.

```tsx
let changingString = "Hello World";
changingString = "Olá Mundo";
// Because `changingString` can represent any possible string, that
// is how TypeScript describes it in the type system
changingString;
      
let changingString: string
 
const constantString = "Hello World";
// Because `constantString` can only represent 1 possible string, it
// has a literal type representation
constantString;
      
const constantString: "Hello World"
```

By themselves, literal types aren’t very valuable:

```tsx
let x: "hello" = "hello";
// OK
x = "hello";
// ...
x = "howdy";
Type '"howdy"' is not assignable to type '"hello"'.
```

It’s not much use to have a variable that can only have one value!

But by *combining* literals into unions, you can express a  much more useful concept - for example, functions that only accept a  certain set of known values:

```tsx
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre");
Argument of type '"centre"' is not assignable to parameter of type '"left" | "right" | "center"'.
```

There’s one more kind of literal type: boolean literals. There are only two boolean literal types, and as you might guess, they are the types `true` and `false`. The type `boolean` itself is actually just an alias for the union `true | false`.

**Literal Inference**

When you initialize a variable with an object, TypeScript assumes that the properties of that object might change values later. For example, if you wrote code like this:

```tsx
const obj = { counter: 0 };
if (someCondition) {
  obj.counter = 1;
}
```

TypeScript doesn’t assume the assignment of `1` to a field which previously had `0` is an error. Another way of saying this is that `obj.counter` must have the type `number`, not `0`, because types are used to determine both *reading* and *writing* behavior.The same applies to strings:

```tsx
declare function handleRequest(url: string, method: "GET" | "POST"): void;
 
const req = { url: "https://example.com", method: "GET" };
handleRequest(req.url, req.method);
Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.
```

In the above example `req.method` is inferred to be `string`, not `"GET"`. Because code can be evaluated between the creation of `req` and the call of `handleRequest` which could assign a new string like `"GUESS"` to `req.method`, TypeScript considers this code to have an error.

There are two ways to work around this.

1. You can change the inference by adding a type assertion in either location:

```tsx
// Change 1:
const req = { url: "https://example.com", method: "GET" as "GET" };
// Change 2
handleRequest(req.url, req.method as "GET");
```

Change 1 means “I intend for `req.method` to always have the *literal type*`"GET"`”, preventing the possible assignment of `"GUESS"` to that field after. Change 2 means “I know for other reasons that `req.method` has the value `"GET"`“.

You can use `as const` to convert the entire object to be type literals:

```tsx
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);
```

The `as const` suffix acts like `const` but for the type system, ensuring that all properties are assigned the literal type instead of a more general version like `string` or `number`.

**`null` and `undefined`**

JavaScript has two primitive values used to signal absent or uninitialized value: `null` and `undefined`.

TypeScript has two corresponding *types* by the same names. How these types behave depends on whether you have the `strictNullChecks` option on.

**`strictNullChecks` off**

With `strictNullChecks` *off*, values that might be `null` or `undefined` can still be accessed normally, and the values `null` and `undefined` can be assigned to a property of any type. This is similar to how languages without null checks (e.g. C#, Java) behave. The lack of checking for these values tends to be a major source of bugs; we always recommend people turn `strictNullChecks` on if it’s practical to do so in their codebase.

**`strictNullChecks` on**

With `strictNullChecks` *on*, when a value is `null` or `undefined`, you will need to test for those values before using methods or properties on that value. Just like checking for `undefined` before using an optional property, we can use *narrowing* to check for values that might be `null`:

```tsx
function doSomething(x: string | null) {
  if (x === null) {
    // do nothing
  } else {
    console.log("Hello, " + x.toUpperCase());
  }
}
```

**Non-null Assertion Operator (Postfix `!`)**

TypeScript also has a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`:

```tsx
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
Try
```

**Enums**

Enums are a feature added to JavaScript by TypeScript which allows  for describing a value which could be one of a set of possible named  constants. Unlike most TypeScript features, this is *not* a  type-level addition to JavaScript but something added to the language  and runtime. Because of this, it’s a feature which you should know  exists, but maybe hold off on using unless you are sure. You can read  more about enums in the **[Enum reference page](https://www.typescriptlang.org/docs/handbook/enums.html).**

## Less Common Primitives

It’s worth mentioning the rest of the primitives in JavaScript which are represented in the type system. Though we will not go into depth here.

### `bigint`

From ES2020 onwards, there is a primitive in JavaScript used for very large integers, `BigInt`:

Narrowing

Imagine we have a function called `padLeft`.

```tsx
function padLeft(padding: number | string, input: string): string {
  throw new Error("Not implemented yet!");
}
```

If `padding` is a `number`, it will treat that as the number of spaces we want to prepend to `input`. If `padding` is a `string`, it should just prepend `padding` to `input`. Let’s try to implement the logic for when `padLeft` is passed a `number` for `padding`.

```tsx
function padLeft(padding: number | string, input: string): string {
  return " ".repeat(padding) + input;
Argument of type 'string | number' is not assignable to parameter of type 'number'.
  Type 'string' is not assignable to type 'number'.
```

[theory of typescript](https://www.notion.so/theory-of-typescript-1b47af54188580d7a822e5804f79161e?pvs=21)