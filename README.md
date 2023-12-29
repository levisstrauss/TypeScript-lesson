### This is the TypeScript lesson series
    TypeScript is a superset of JavaScript that compiles to plain JavaScript. It offers classes, 
    modules, and interfaces to help you build robust components. The TypeScript language 
    specification has full details about the language.
    Benefits of TypeScript:
      - Static typing
      - Class-based object-oriented programming
      - Code completion 
      - Refactoring
      - Shorthand notations
---
### Environment set up
    - Install Node.js
    - Install TypeScript: npm install -g typescript
    - tsc -v (check version)
    - tsc (compile ts file): tsc main.ts
    - Run javascript file: node dist/main.js
---
### TypeScript Configuration
    - tsc --init (create tsconfig.json)
    - tsc (compile all ts files): tsc
    - tsc -w (watch mode)
    - tsc -w -p (watch mode with tsconfig.json)

    ---- Configuration Options ----
    - target: Specify ECMAScript target version: "ES3" (default), 
      "ES5", "ES6"/"ES2015", "ES2016", "ES2017", "ES2018", "ES2019", "ES2020", "ESNext"

    --------- Module---------
       - "rootDir": "./src",  (default) directory that contain our source file

    ---------- Emit ----------
       - "outDir": "./dist", (default) directory that contain our output file
       - "removeComments": true, (default) remove all comments in js file
       - "noEmitOnError": true, (default) don't emit js file if there is an error in ts file
       - "sourceMap": true,      Create source map files for emitted JavaScript files. that will
                                 create a .map file for each .js file helping us to debug our code.

    ---------- Type Checking ----------
      - "noUnusedParameters": true, Raise an error when a function parameter isn't read.
      - "noImplicitReturns": true, Enable error reporting for codepaths that do not explicitly return in a function.
      - "noUnusedLocals": true, Enable error reporting when local variables aren't read.
      - "noImplicitOverride": true, Ensure overriding members in derived classes are marked with an override modifier.

    --------- Labguage and environment ------
       - "experimentalDecorators": true,  Enable experimental support for legacy experimental decorators.

    NB: Now to compile our code we only need to type tsc in the terminal
---
### Fundamentals 
    - The any type  - Enums
    - Arrays        - Functions
    - Tuples        - Objects
    - Typescript Types: any, unknown, never, enum, tuple
       

### Variables: Use variables to store values
```typescript
   let sales = 123_456_489;
   let course = "TypeScript";
   let is_published = true;
   let level; // type => any
```

### Arrays: Use arrays to store collections of data
```typescript
   let course: string[] = ["TypeScript", "JavaScript", "React"];
   let numbers: number[] = [1, 2, 3, 4, 5];
   let courses: any[] = ["TypeScript", 123, true];
   
   //---- Arrays Methods ----
    courses.push("React"); // add element at the end of the array
    courses.pop();         // remove element at the end of the array
    courses.shift();       // remove element at the beginning of the array
    courses.unshift("React"); // add element at the beginning of the array
    courses.splice(2, 0, "React"); // add element at the index 2

   //---- Array Iteration ----
    for (let course of courses) {
        console.log(course);
    }
    courses.forEach((course, index) => console.log(index, course));
    courses.forEach((course, index) => console.log(index, course));
    courses.forEach((course, index) => console.log(index, course));
```

### Tuples: Use tuples when you know the exact number of elements in an array
```typescript
   let person: [string, number, boolean] = ["John", 22, true];
   person[0] = "John";
   person[1] = 22;
   person[2] = true;
   
   personal[0].toLowerCase(); // John
   personal[1].toFixed(2);    // 22.00
   personal[2].valueOf();     // true
    //---- Tuple Iteration ----
   person.forEach((person, index) => console.log(index, person));
     
```

### Enum
```typescript
   const enum Color {Red, Green, Blue};
   let myColor: Color = Color.Green;
   let backgroundColor = Color.Red;
   console.log(backgroundColor); // 0
   console.log(Color[backgroundColor]); // Red

   enum Color {Red = 0, Green = 1, Blue = 2}; // Those numbers are optional  
    
```

### Functions: Use functions to avoid code duplication
```typescript
   function add(x: number, y: number): number {
       return x + y;
   }
   let result1 = add(5, 10);
   console.log(result); // 15

   //---- Optional Parameters ----
   function add(x: number, y?: number): number {
       return x + y;
   }
   let result2 = add(5);
   console.log(result); // NaN

   //---- Default Parameters ----
   function add(x: number, y: number = 10): number {
       return x + y;
   }
   let result3 = add(5);
   console.log(result); // 15

   //---- Rest Parameters ----
   function add(x: number, ...y: number[]): number {
       return x + y;
   }
   let result4 = add(5, 10, 20, 30);
   console.log(result); // 65

   //---- Function Overloading ----
   function add(x: number, y: number): number;
   function add(x: string, y: string): string;
   function add(x: any, y: any): any {
       return x + y;
   }
   let result5 = add(5, 10);
   console.log(result); // 15
   let result6 = add("5", "10");
   console.log(result); // 510

   function calculateTax(income: number, taxYear = 2022): number {
       if (taxYear < 2022) 
           return income * 0.4;
       return income * 0.3;
   }
   
   calculateTax(50000); // 15000
```

### Objects: Use objects to model real-world entities
```typescript
   let person = {
       name: "John",
       age: 22,
       isMarried: true
   };
   person.name = "John";
   person.age = 22;
   person.isMarried = true;
   console.log(person.name); // John
   console.log(person.age); // 22
   console.log(person.isMarried); // true

   //---- Object Iteration ----
   for (let key in person) {
       console.log(key, person[key]);
   }
   for (let key of Object.keys(person)) {
       console.log(key, person[key]);
   }
   for (let entry of Object.entries(person)) {
       console.log(entry);
   }
   for (let value of Object.values(person)) {
       console.log(value);
   }
   
   //---- Object with type ----
    let employee: {
         readonly id: number,
         name: string,
         age: number,
         isMarried: boolean,
         retire: (date: Date) => void
    } = {
        id: 1,
        name: "John",
        age: 22,
        isMarried: true, 
        retire: (date: Date) => {
            console.log("Retired on " + date);
        }
    };
    employee.name = "John";
    employee.age = 22;
    employee.isMarried = true;
    employee.retire(new Date());
    // --- execute function ---
    employee.retire(new Date());
```
---
### Advanced Types: Use advanced types to make your code more expressive
    - Type aliases, Unions and intersections, Type narrowing
    - Nulllable types, the unknown type, the never type
```typescript
type Employee = {
    readonly id: number,
    name: string,
    age: number,
    isMarried: boolean,
    retire: (date: Date) => void
};
let employee: Employee = {
        id: 1,
        name: "John",
        age: 22,
        isMarried: true, 
        retire: (date: Date) => {
            console.log("Retired on " + date);
        }
    };
```

### Union types: combine multiple types
```typescript
function kgToLbs(weight: number | string): number {
    if (typeof weight === "number") 
        return weight * 2.2;
    else
        return parseInt(weight) * 2.2; 
}
kgToLbs(70); // 154
kgToLbs("70"); // 154
```

### Intersection types: combine multiple types
```typescript

type Draggagle = {
    drag: () => void
};

type Resizable = {
    resize: () => void
};
type UIWidget = Draggagle & Resizable;

let textBox: UIWidget = { // textBox must have drag and resize methods
    drag: () => {
        console.log("Draggable");
    },
    resize: () => {
        console.log("Resizable");
    }
};
```

### Literal types: Use literal types to specify exact values
```typescript
  type Quantity = 50 | 100 | 300;
  let quantity: Quantity = 50 | 100 | 300; // quantity must be 50 or 100 or 300
  
  // direction must be left or right or top or bottom 
  type Direction = "left" | "right" | "top" | "bottom";
  let direction: Direction = "left" | "right" | "top" | "bottom"; 
```

### Type Guards: Use type guards to narrow down types
```typescript
  type Employee = {
    id: number,
    name: string,
    age: number,
    isMarried: boolean,
    retire: (date: Date) => void
  };
  type Customer = {
    id: number,
    name: string,
    age: number,
    isMarried: boolean,
    credit: number
  };
  type Person = Employee | Customer;
  function printDetails(person: Person) {
    if ("retire" in person) {
        console.log(person.retire(new Date()));
    } else {
        console.log(person.credit);
    }
  }
```

### Nullable types: Use nullable types to allow null values
```typescript
  let quantity: number | null = 50;
  quantity = null;
```

### The unknown type: Use the unknown type to represent dynamic values
```typescript
  let quantity: unknown = 50;
  quantity = "50";
  quantity = true;
```

### The never type: Use the never type to represent unreachable code
```typescript
  function throwError(message: string): never {
    throw new Error(message);
  }
  function infiniteLoop(): never {
    while (true) {
        console.log("Hello");
    }
  }
```
### Optional Types: Use optional types to make properties optional
```typescript
  type Employee = {
    id: number,
    name: string,
    age: number,
    isMarried?: boolean,
    retire: (date: Date) => void
  };
  let employee: Employee = {
    id: 1,
    name: "John",
    age: 22,
    retire: (date: Date) => {
        console.log("Retired on " + date);
    }
  };
```
### Type Assertions: Use type assertions to tell the compiler about the type of a value
```typescript
  let message;
  message = "abc";
  let endsWithC = (<string>message).endsWith("c");
  let alternativeWay = (message as string).endsWith("c");
```
---
### Classes: Use classes to create objects with properties and methods
```typescript
  class Employee {
    id: number;
    name: string;
    age: number;
    isMarried: boolean;
    constructor(id: number, name: string, age: number, isMarried: boolean) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.isMarried = isMarried;
    }
    retire(date: Date) {
        console.log("Retired on " + date);
    }
  }
  let employee = new Employee(1, "John", 22, true);
  employee.retire(new Date());
```
— Using Access Modifiers ----

```typescript
  class Account {
    readonly id: number;
    owner: string;
    private _balance: number;
    nickname?: string; // optional property
    // Constructor
    constructor(id: number, owner: string, balance: number) {
        this.id = id;
        this.owner = owner;
        this.balance = balance;
 
    }
    // Methods
    deposit(amount: number): void {
        if (amount <= 0) {
            throw new Error("Deposit amount has to be greater than 0");
        }
        this.balance += amount;
    }
    // Private method
    private withdraw(amount: number): void {
        if (amount <= 0) {
            throw new Error("Withdraw amount has to be greater than 0");
        }
        this.balance -= amount;
    }
    
    // Getters and Setters
    // Getters and Setters
    get balance(): number {
        return this._balance;
    }
    set balance(value: number): void {
        if (value <= 0) {
            throw new Error("Balance has to be greater than 0");
        }
        this._balance = value;
    }
  }
   let account = new Account(1, "Zakaria", 0);
   account.deposit(100);
   console.log(account.getBalance()); // 100
   account.withdraw(50); // Error: Property 'withdraw' is private and 
                         // only accessible within class 'Account'
```
— Using parameter properties ----
```typescript
  class Account {
    // Constructor
    constructor(
        readonly id: number,
        public owner: string,
        private _balance: number,
        public nickname?: string
    ) {}
    // Methods
    deposit(amount: number): void {
        if (amount <= 0) {
            throw new Error("Deposit amount has to be greater than 0");
        }
        this.balance += amount;
    }
    // Getters and Setters
    get balance(): number {
        return this._balance;
    }
    set balance(value: number): void {
        if (value <= 0) {
            throw new Error("Balance has to be greater than 0");
        }
        this._balance = value;
    }
  }
   let account = new Account(1, "Zakaria", 0);
   account.deposit(100);
   console.log(account.balance()); // 100
   
```
### Index Signature 
```typescript
class SeatAssignment {
    [seatNumber: string]: string; // Index signature
}
let seat = new SeatAssignment();
seat["34D"] = "Zakaria";
seat["34E"] = "John";
   
```
### Static members: Use static members to define properties and methods that belong to a class
```typescript
  class Ride {
   private static _activeRides: number = 0; // To create a single instance of a property in memory
    
    start() {
        Ride.activeRides++;
    }
    stop() {
        Ride.activeRides--;
    }
    static get activeRides() {
        return Ride._activeRides;
    }
  }
  
  let ride1 = new Ride();
  ride1.start();
  let ride2 = new Ride();
  ride2.start();
  
  console.log(Ride.activeRides); // 2
   
```
### Inheritance: Use inheritance to create a class hierarchy
```typescript
  class Person {
    constructor(public firstName: string, lastName: String) {}
    walk() {
        console.log("Walking");
    }
    get fullName() {
        return this.firstName + " " + this.lastName;
    }
  }
  
  
  class Student extends Person {
    constructor(public studentId: number, firstName: string, lastName: String) {
        super(firstName, lastName);
        this.studentId = studentId;
    }
    takeTest() {
        console.log("Taking test");
    }
    
  }
  let student = new Student(1, "Zakaria", "Hassan");
    student.walk();
    student.takeTest();
    
  // ---- Method Overriding ----
class Teacher extends Person {
    override get fullName(){
        return "Professor ' + " + super.fullName;
    }
}
```
### Polymorphism: Use polymorphism to create a single interface to entities of different types
```typescript

class Person {
    constructor(public firstName: string, lastName: String) {}
    walk() {
        console.log("Walking");
    }
    get fullName() {
        return this.firstName + " " + this.lastName;
    }
}
    
class Teacher extends Person {
   override get fullName(){
      return "Professor ' + " + super.fullName;
  }
}

class Principal extends Person {
    override get fullName(){
        return "Principal ' + " + super.fullName;
    }
}

printNames([
    new Student(1, "Zakaria", "Hassan"),
    new Teacher("John", "Doe"),
    new Principal("Jane", "Doe")
]);

function printNames(people: Person[]) {
    for (let person of people) {
        console.log(person.fullName);
    }
}

```
### Abstract classes: Use abstract classes to define a common interface for subclasses
```typescript

// Abstract class
abstract class Shape {
constructor(public color: string) {}
    // Abstract method
   abstract render(): void;
}

class Circle extends Shape {
    constructor(color: string, public radius: number) {
        super(color);
    }
    
    render() {
        console.log("Drawing a circle");
    }
}
```

### Interfaces: Use interfaces to define a shape or contract for classes to implement
```typescript

interface Calendar {
   name : string;
   addEvent(): void;
   removeEvent(): void;
}

interface CloudCalendar extends Calendar {
   sync(): void;
}

class GoogleCalendar implements CloudCalendar {
    constructor(public name: string){}
    addEvent() {
        console.log("Event added");
    }
    removeEvent() {
        console.log("Event removed");
    }
    sync() {
        console.log("Syncing");
    }
}
```
---
### Generics: Use generics to create reusable components
```typescript
------- Array -------
let numbers: number[] = [1, 2, 3];
```
```typescript
-------- Generic class------
class KeyValuePair<K, V> {
    constructor(public key: K , public value: V) {}
}

let pair = new KeyValuePair<string, string>('1', "First");
```
```typescript
-------- Generic function------
function wrapInArray<T>(value: T) {
    return [value];
}

let numbers = wrapInArray(1);
let strings = wrapInArray("Hello");

----- The function can be inside of a class -----
 class ArrayUtils {
    static wrapInArray<T>(value: T) {
        return [value];
    }
 }
 let numbers = ArrayUtils.wrapInArray(1);
```
```typescript
-------- Generic interface ------
https:///myapi.com/api/v1/employees

interface Result<T> {
    data: T | null;
    error: string | null;
}

function fetch<T>(url: string): Result<T> {
    return {
        data: "Data",
        error: null
    };
}
--------------
interface User {
    id: number;
    name: string;
    age: number;
    isMarried: boolean;
}
interface Product {
    id: number;
    name: string;
    price: number;
    description: string;
}

let result = fetch<User>("https:///myapi.com/api/v1/employees");
result.data // will be a User object

let result = fetch<Product>("https:///myapi.com/api/v1/products");
result.data // will be a Product object

```
---
### Decorators: Use decorators to add metadata to classes and class members
```typescript
------ Decorator without parameter ------
function Component() {
    return function (target: any) {
        console.log("Component");
    };
}

@Component
class ProfileComponent {}

------ Decorator with parameter ------
function Component(value: number) {
    return function (target: any) {
        console.log("Component");
    };
}

@Component(1)
class ProfileComponent {}
  
------ Multiple decorator  ------
function Component1() {
}
function Component2() {
 
}
@Component1()
@Component1()
class ProfileComponent {}
```
---
### Modules: Use modules to organize your code
```typescript
Exporting and importing
// shapes.ts
export class Circle {}
export class Square {}
// app.ts
import { Circle, Square as MySquare } from './shapes';
Default exports
// shapes.ts
export default class Circle {}
// app.ts
import Circle from './shapes';
Wildcard imports
// app.ts
import * as Shapes from './shapes';
let circle = new Shapes.Circle();
Re-exporting
// /shapes/index.ts
export { Circle } from './circle';
export { Square } from './square';
// app.ts
import { Circle, Square } from './shapes';
```
