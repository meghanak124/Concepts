# Javascript Technical Paper
## Different datatypes in JavaScript
![](https://www.w3schools.com/js/img_datatypes_500.jpg)
## Scopes in javaScript
- var is function scoped
- let and const are block scoped
1. Global 
```js
// Global Variable accessed from within a function 
const x = 10;
function fun1() {
    console.log(x);
}
fun1();
```
2. Local
```js
function fun2(){ 
    // This variable is local to fun2() and 
    // cannot be accessed outuside this function
    let x = 10;
    console.log(x);
}
fun2();
```
3. Block 
```js
{
    // Var can Accessible inside & outside the block scope 
    var x = 10; 
    // let , const Accessible only inside the block scope
    const y = 20;
    let z = 30;
    console.log(x);
    console.log(y);
    console.log(z);
}
console.log(x);
```
4. Lexical: The variable is declared inside the function and can only be accessed inside that block or nested block is called lexical scope.
```js
function func1() {
    const x = 10;
    function func2() {
        const y = 20;
        console.log(`${x} ${y}`);
    }
    func2();
}
func1();
```
## var, let and const
-  Use const by default for everything. Only switch to let if you know the value needs to change (like a counter in a loop). Avoid var entirely.

Feature	| var	| let	| const
| -------- | -------- | -------- | -------- | 
Scope	| Function Scope	| Block Scope	| Block Scope
Hoisting	| Yes (as undefined)	| Yes (Temporal Dead Zone)	| Yes (Temporal Dead Zone)
Reassignable	| Yes	| Yes	| No
Redeclarable	| Yes	| No	| No

## why we must not use var
1. var is function-scoped, meaning it ignores blocks like if statements or for loops. This can lead to variables "leaking" out and causing unintended side effects.
```js
if (true) {
  var color = "red";
}
console.log(color); // Prints "red" (Wait, it should be private to the IF block!)
```
2. Hoisting and the "Undefined" Trap
```js
console.log(user); // Returns undefined (Confusing!)
var user = "Alice";
```
3. Accidental Redeclaration
```js
var score = 10;
// ... 100 lines of code later ...
var score = 100; // No error, just overwrites the original.
```
## Why using global variables is bad
**1. Name Collisions (Naming Conflicts)**

Global variables live in a shared space (the window object in browsers). If two different scripts or libraries use the same variable name (e.g., const data = ...), one will overwrite the other, leading to silent bugs that are incredibly hard to track down.

**2. Security Risks**

Because global variables are accessible from anywhere, any script running on your page—including third-party ads or malicious tracking scripts—can read or modify your sensitive data.

**3. Difficult Debugging & Testing**

When a variable is global, any function in your entire codebase can change its value at any time.
If your app crashes because a variable has the wrong value, you have to search your entire project to find which line of code changed it.
In local scope, you only have to check the few lines within that function or block.

**4. "Spaghetti Code" (High Coupling)**

Global variables create hidden dependencies between unrelated parts of your code. If you change a global variable to fix a bug in "Feature A," you might accidentally break "Feature B" because it relied on that same variable. This makes your code fragile.

**5. Memory Management**
Local variables are "cleaned up" (garbage collected) by the browser as soon as a function finishes running. Global variables stay in memory until the page is closed or refreshed, which can lead to memory leaks in large applications.

## Truthy and Falsy values
- The Falsy Values

There are only 8 values in JavaScript that are falsy. If it's not on this list, it’s truthy.
1. false: The keyword itself.
2. 0: The number zero.
3. -0: Negative zero.
4. 0n: BigInt zero.
5. "": An empty string (no space).
6. null: Explicitly "nothing."
7. undefined: Unassigned variables.
8. NaN: Not-a-Number.

- The Truthy Values
Basically everything else. This includes some values that might surprise you:
1. "0": A string containing a zero.
2. "false": The string "false".
3. []: An empty array.
4. {}: An empty object.
5. function() {}: Empty functions.

The most common bugs come from forgetting that [], {}, "0", and "false" are all truthy, and that 0 and "" are falsy.
```js
// Use Boolean() or !! to explicitly check a value's truthiness:
Boolean(0);      // false
Boolean("");     // false
Boolean([]);     // true
Boolean({});     // true
!!"hello";       // true
!!null;          // false
!!0;             // false
!!"0";           // true  
0 == false        // true  
"" == false       // true
null == false     // false null only == undefined
null == undefined // true
[] == false       // true  
```
## Function hoisting
- Hoisting refers to the behavior where JavaScript moves the declarations of variables, functions, and classes to the top of their scope during the compilation phase. 
- Initializations are not hoisted; they are only declarations.
- 'var' variables are hoisted with undefined, while 'let' and 'const' are hoisted but remain in the Temporal Dead Zone until initialized.
- TEMPORAL DEAD ZONE : Variables declared with let and const are hoisted to the top of their scope, but they are not initialized until their declaration line is reached.
```js
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;

greet(); // "Hello, Mahima!"
function greet() {
    console.log("Hello, Mahima!");
}

hello(); // TypeError: hello is not a function
var hello = function() {
    console.log("Hi!");
};

function test() {
    console.log(x); // ReferenceError: Cannot access 'x' before initialization
    let x = 50;
}
test();

const obj = new MyClass(); // ReferenceError
class MyClass {
    constructor() {
        this.name = "Mahima Bhardwaj";
    }
}

var a = 10;
var a = 20; // No error
console.log(a); // 20

for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i); // 3, 3, 3
    }, 100);
}

test(10); // 10
function test(num) {
    console.log(num);
}

function outer() {
    console.log(a); // undefined
    var a = 5;
    function inner() {
        console.log(b); // undefined
        var b = 10;
    }
    inner();
}
outer();
```
## What happens when a function does not have a return statement
- When a function does not have a return statement, it automatically returns undefined by default.
- In JavaScript, every function call must result in a value. If you don't specify one, the engine effectively adds return undefined; to the very end of your function body
```js
function logMessage(msg) {
  console.log(msg); 
  // No return here
}
const result = logMessage("Hello");
console.log(result); // Output: undefined

function checkAge(age) {
  if (age < 18) return; // Exits early
  return "Welcome!";
}
console.log(checkAge(10)); // Output: undefined
```
- ARROW FUNCTIONS:
```js 
// Implicit (Returns value): 
const add = (a, b) => a + b; //(Returns the sum)
// Explicit (Returns undefined): 
const add = (a, b) => { a + b }; // (Returns undefined because of the braces)
  ```
  ## Different ways of declaring a function
  - mainly there are 3 ways: Function Declaration, Function Expression, Arrow Functions
  1. Function declaration
  ```js
  function greet(name) {
    return `Hello, ${name}!`;
  }
```
2. Function Expression
```js
const add = function(a, b) {
  return a + b;
};
```
3. Arrow Function (ES6)
```js
const multiply = (a, b) => a * b; // Implicit return for single-line
```
4. Shorthand Method Definition
```js
const calculator = {
  sum(a, b) {
    return a + b;
  }
};
```
5. Immediately Invoked Function Expression (IIFE)
```js
(function() {
  console.log("I run immediately!");
})();
```
6. Constructor Function
```js
function Person(name) {
  this.name = name;
}
const user = new Person("Alice");
```
## Pass by reference and pass by value - add codeblocks
1. Pass by Value (Primitives)
```js
let score = 100;
function updateScore(value) {
  value = 200; // Only the local copy changes
  console.log("Inside function:", value); // 200
}
updateScore(score);
console.log("Outside function:", score); // 100 (Unchanged)
```
2. Pass by Reference (Objects/Arrays)
```js
let user = { name: "Alice" };
function renameUser(obj) {
  obj.name = "Bob"; // Modifies the actual object in memory
  console.log("Inside function:", obj.name); // "Bob"
}
renameUser(user);
console.log("Outside function:", user.name); // "Bob" (Changed!)
```
- Reassignment Catch
```js
let colors = ["red", "blue"];
function replaceColors(arr) {
  arr = ["green", "yellow"]; // Reassigning to a NEW array
  console.log("Inside function:", arr); // ["green", "yellow"]
}
replaceColors(colors);
console.log("Outside function:", colors); // ["red", "blue"] (Unchanged!)
```
## Different types of for loops - for with numbers, for..in, for..of, forEach, while
1. for Loop (with Numbers/ range)
```js
const fruits = ["apple", "banana", "cherry"];
for (let i = 0; i < fruits.length; i++) {
  console.log(i, fruits[i]); // 0 apple, 1 banana...
}
```
2. for...of (Arrays & Iterables)
```js
const colors = ["red", "green", "blue"];
for (const color of colors) {
  console.log(color); // red, green, blue
}
```
3. for...in (Object Properties)
```js
const user = { name: "Alice", age: 25 };
for (const key in user) {
  console.log(key, user[key]); // name Alice, age 25
}
```
4. forEach() (Array Method like enumerate)
```js
const nums = [10, 20, 30];
nums.forEach((num, index) => {
  console.log(`Index ${index}: ${num}`);
});
```
5. while & do...while (Condition-based)
```js
let power = 1;
while (power < 10) {
  console.log(power);
  power *= 2; // 1, 2, 4, 8
}
```
## Searching mdn (mozilla developer network)
- MDN is the "gold standard" for JavaScript documentation. 
- To use it like a pro, focus on these three layers:

**1. The Two Main Paths**

**The Guide:** Best for learning concepts (e.g., "How do Closures work?"). [Explore the Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide).

**The Reference:** Best for technical facts (e.g., "What are the parameters for Array.map()?"). [View the Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference).

**2. Essential Page Features**

**Interactive Playground:** Most JS pages have a "Try it" box to run code live in the browser.

**Browser Compatibility:** Every page ends with a table showing exactly which version of Chrome, Firefox, or Safari supports that feature .

**Specifications:** Links directly to the official ECMAScript standard for deep technical proof.

**3. Searching**

**Direct URL:** Type developer.mozilla.org/ followed by the term (e.g., /docs/Web/JavaScript/Reference/Global_Objects/Array/reduce).

**Browser Shortcut:** In Firefox, type @mdn [term] in the address bar for instant results.
Google Hack: Search mdn [feature] (e.g., mdn fetch) to skip the landing page and go straight to the technical docs.

## Popular array utility methods - add codeblocks and mention mutable/immutable
```js
- Basics
//mutable
const arr = [1, 2];
arr.push(3); // [1, 2, 3]
arr.pop();    // [1, 2]
const nums = [1, 2, 3];
nums.splice(1, 1, 'x'); // [1, 'x', 3]
```

```js
// immutable
const a = [1];
const b = [2];
const c = a.concat(b); // [1, 2]
const letters = ['a', 'b', 'c'];
const part = letters.slice(0, 2); // ['a', 'b']
const words = ['Hello', 'World'];
const str = words.join(' '); // "Hello World"
const nested = [1, [2, [3]]];
const flat = nested.flat(2); // [1, 2, 3]
```

- finding
```js 
///finding are all immutable
[10, 20, 30].indexOf(20); // 1

['apple', 'orange'].includes('apple'); // true

const users = [{id: 1, name: 'A'}, {id: 2, name: 'B'}];
const user = users.find(u => u.id === 2); // {id: 2, name: 'B'}

[5, 12, 8].findIndex(n => n > 10); // 1
```
- Higher Order Functions:
```js
const fruits = ["apple", "banana", "cherry"];
fruits.forEach((fruit) => {
  console.log(`I love ${fruit}!`);
});
// Output: 
// I love apple!
// I love banana!
// I love cherry!

const evens = [1, 2, 3, 4].filter(n => n % 2 === 0); // [2, 4]

const doubled = [1, 2].map(n => n * 2); // [2, 4]

const sum = [1, 2, 3].reduce((acc, curr) => acc + curr, 0); // 6

const unsorted = [3, 1, 2];
unsorted.sort(); // [1, 2, 3]
```
4. Array methods chaining
```js
const products = [
  { name: 'Shirt', price: 20, available: true },
  { name: 'Pants', price: 40, available: false },
  { name: 'Hat', price: 15, available: true }
];
// Chain: Filter -> Map -> Sort
const result = products
  .filter(p => p.available)        // Only available items
  .map(p => p.name.toUpperCase())  // Get names in Uppercase
  .sort();                         // Sort alphabetically
console.log(result); // ["HAT", "SHIRT"]
```
## When to use forEach, when to use array utility methods like map, filter, reduce
```js
const products = [
  { id: 1, name: "Laptop", price: 1000, inStock: true },
  { id: 2, name: "Mouse", price: 25, inStock: false },
  { id: 3, name: "Monitor", price: 200, inStock: true }
];

// map(): Transform Data
const productNames = products.map(item => item.name); // Result: ["Laptop", "Mouse", "Monitor"]

// filter(): Select a Subset
const availableItems = products.filter(item => item.inStock === true); // Result: [{id: 1, name: "Laptop"...}, {id: 3, name: "Monitor"...}]

// reduce(): Calculate a Single Total
const totalBill = products.reduce((total, item) => total + item.price, 0); // Result: 1225

// forEach(): Perform an Action
products.forEach(item => {
  console.log(`Product: ${item.name} costs $${item.price}`);
});
```
## Error handling (try catch)

**Key Components**

**try:** Tests a block of code for errors.

**catch(error):** Catches the error object. This object usually has a .message (description) and a .name (type of error).

**finally:** (Optional) Runs after try and catch, regardless of the result. It is perfect for closing database connections or hiding loading spinners.

**throw:** Allows you to create custom errors.

```js
try {
  // Code that might fail
  const data = JSON.parse("invalid-json"); 
} catch (error) {
  // Handle the error
  console.error("Oops! Something went wrong:", error.message);
} finally {
  // Always runs, regardless of whether an error occurred
  console.log("Cleanup complete.");
}
```
## Throwing errors
```js
function checkAge(age) {
  if (age < 18) {
    throw new Error("You must be 18 or older.");
  }
  return "Access granted!";
}
try {
  console.log(checkAge(15));
} catch (err) {
  console.log(err.name);    // "Error"
  console.log(err.message); // "You must be 18 or older."
}
```
## Difference between throw new Error("Error message here") and throw "Error message here
**1. throw new Error("...") (The Right Way)**

When you use the Error constructor, you create a rich Error Object.

**Stack Trace:** It automatically captures a "stack trace," which tells you exactly which file and which line number caused the problem. This is vital for debugging.

**Properties:** It provides useful properties like .message (the text you passed in) and .name (e.g., "Error", "TypeError") 
```js
try {
  throw new Error("Something went wrong!");
} catch (err) {
  console.log(err.name);    // "Error"
  console.log(err.message); // "Something went wrong!"
  console.log(err.stack);   // Detailed list of where the error happened
}
```
**throw "..." (The "Lazy" Way)**

**No Stack Trace:** You lose all information about where the error occurred in your code.

**Harder to Handle:** Since it’s just a string, you can't access .message or .name. If your catch block expects an object, your code might crash trying to read err.message from a string
```js
try {
  throw "Something went wrong!";
} catch (err) {
  console.log(err);         // "Something went wrong!"
  console.log(err.message); // undefined (Strings don't have a .message property)
  console.log(err.stack);   // undefined
}
```
## Reading error messages and tracing issues from the stack trace when errors happen - practice this daily for 2 weeks with different examples. this is very important
```js
function getUsername(user) {
  return user.name.toUpperCase(); // ❌ Error here if user is null
}
function processLogin(data) {
  return getUsername(data);
}
try {
  processLogin(null);
} catch (err) {
  console.log(err.stack);
}
// The resulting Stack Trace looks like this:
/*  TypeError: Cannot read properties of null (reading 'name')
    at getUsername (app.js:2:19)
    at processLogin (app.js:6:10)
    at app.js:10:3
*/
```
## Importance of catch block
1. if an error occurs → execution stops immediately
```js 
// Without catch, 
console.log("Start");
let result = 10 / x; // x is not defined → ERROR
console.log("End"); // ❌ never runs
/*  OUTPUT
Start
ReferenceError */

// With catch,
console.log("Start");

try {
  let result = 10 / x;
} catch (error) {
  console.log("Error handled:", error.message);
}
console.log("End");
/*
Start
Error handled: x is not defined
End */ => 2. keeps application flow
```
3. Gives control over errors
4. Helps debugging
```js
try {
  let num = undefinedVariable;
} catch (error) {
  console.log(error.name);    // ReferenceError
  console.log(error.message); // undefinedVariable is not defined
}
```
## Template literals
**1. String Interpolation**
```js
const name = "Alice";
const score = 10;
// Old way
console.log("Player " + name + " has " + (score * 10) + " points.");
// Template Literal
console.log(`Player ${name} has ${score * 10} points.`);
```
**2. Multi-line Strings**
```js
// This works exactly as it looks
const message = `Hello,
This is a message
on multiple lines!`;
```
**3. Expressions inside ${}**
```js
const price = 100;
const tax = 0.1;
console.log(`Total Price: $${(price * (1 + tax)).toFixed(2)}`); 
// Output: Total Price: $110.00
```
## Default parameters
```js
const getDefaultTax = () => 0.15;
function greet(name = "Guest", price= 40, tax = getDefaultTax()) {
  console.log(`Hello ${name}, your tax is ${price + tax}.`);
}
greet("Meghana", 30); // Hello Meghana, your tax is 30.15.
greet();          // "Hello Guest, your tax is 40.15.
greet(undefined, 20); // Hello Guest, your tax is 20.15.
```
## Destructuring
Destructuring is a shorthand syntax that lets you "unpack" values from arrays or properties from objects into distinct variables.
**1. Object Destructuring**
```js
const user = { name: "Meghana", age: 20, city: "Bengaluru" };
// The Old Way
const name = user.name;
const age = user.age;
// The Modern Way (Destructuring)
const { name, age, city } = user;
console.log(name); // "Meghana"
```
**2. Array Destructuring**
```js
const colors = ["red", "green", "blue"];
// Skips the second item using a comma
const [primary, , tertiary] = colors;
console.log(primary);  // "red"
console.log(tertiary); // "blue"
```
**3. Renaming & Default Values**
```js
const settings = { theme: "dark" };
// Rename 'theme' to 'currentTheme' and set a default for 'fontSize'
const { theme: currentTheme, fontSize = 14 } = settings;
console.log(currentTheme); // "dark"
console.log(fontSize);     // 14
```
## Closure
A closure is a function that "remembers" the variables from its outer scope, even after that outer scope has finished executing. 
```js
function createGreeter(greeting) {
  // This is the outer scope
  return function(name) {
    // This inner function has a "closure" over 'greeting'
    console.log(`${greeting}, ${name}!`);
  };
}

const sayHello = createGreeter("Hello");
const sayHi = createGreeter("Hi");

sayHello("Meghana"); // "Hello, Meghana!"
sayHi("Sindhu");     // "Hi, Sindhu!"
```
## Arrow functions vs Regular functions
1. The this Binding 

**Regular Functions:** They define their own this based on how the function is called (the "caller").

**Arrow Functions:** They do not have their own this. They inherit this from the surrounding (lexical) scope.
```js
const user = {
  name: "Meghana",
  // Regular Function
  sayHi: function() { 
    console.log(`Hi, I am ${this.name}`); 
  },
  // Arrow Function
  sayHiArrow: () => { 
    console.log(`Hi, I am ${this.name}`); 
  }
};

user.sayHi();      // "Hi, I am Meghana" (this = user)
user.sayHiArrow(); // "Hi, I am undefined" (this = global window object)
```
2. Syntax & Implicit Return
```js
// Regular
function square(n) { return n * n; }

// Arrow (Implicit return - no { } or 'return' needed)
const square = n => n * n;
```
3. The arguments Object

**Regular Functions:** Have an arguments object containing all passed parameters.

**Arrow Functions:** Do not have an arguments object (use Rest Parameters ...args instead).

4. Hoisting

**Regular Functions:** Are fully hoisted. You can call them before they are defined.

**Arrow Functions:** Are not hoisted. They are treated like variables and must be defined before use.

## Difference between === and ==
```js
// 1. == (Loose Equality)
// It checks for Value only.
console.log(5 == "5");    // true (String "5" is converted to Number 5)
console.log(1 == true);   // true (Boolean true is converted to Number 1)
console.log(0 == "");     // true (Both are converted to Number 0)
console.log(null == undefined); // true (Special rule in JS)

// === (Strict Equality)
// It checks for Type + Value.
console.log(5 === "5");   // false (Number vs String)
console.log(1 === true);  // false (Number vs Boolean)
console.log(0 === "");    // false (Number vs String)
console.log(null === undefined); // false (Different types)
```
## Why using value === undefined is better than using !value
**1. The Falsy Value Trap**

When you use !value, JavaScript checks if the value is falsy. There are several values that are "falsy" but are perfectly valid data:
0 (The number zero)
"" (An empty string)
false (The boolean)

```js
function setVolume(level) {
  // Good: Only resets if the user literally didn't provide a value
  if (level === undefined) {
    level = 50;
  }
  console.log(`Volume is: ${level}`);
}
setVolume(0); // Output: "Volume is: 0" (Correct!)

function setVolume(level) {
  // Bad: If level is 0, !level is true, and it resets to 50!
  if (!level) {
    level = 50; 
  }
  console.log(`Volume is: ${level}`);
}
setVolume(0); // Output: "Volume is: 50" (Wrong!)
```
## difference between null and undefined
- **undefined:** Means a variable has been declared but not yet assigned a value. It is JavaScript's default "empty" state.
- **null:** Is an intentional assignment. It is a value that a developer gives to a variable to explicitly say, "this should be empty" or "this value is unknown."
```js
let a;           // undefined (JS did this)
let b = null;    // null (You did this)

console.log(typeof(a))  // undefined
console.log(typeof(b))  // object

console.log(null == undefined);  // true (They are both "falsy" siblings)
console.log(null === undefined); // false (They are different types)

console.log(10 + null);      // 10
console.log(10 + undefined); // NaN
```
## Importing and exporting modules using require and module.exports
```js
// math.js (exporting)
export const PI = 3.14;
export function add(a, b) {
  return a + b;
}
export class Calculator {
  // ...
}

// app.js (importing)
import { PI, add } from './math.js';
console.log(PI); // 3.14
console.log(add(2, 3)); // 5
```
```js
// utils.js (exporting)
function add(a, b) { return a + b; }
const greet = () => "Hello!";
const farewell = () => "Goodbye!";
module.exports = add;
module.exports = { greet, farewell }; // Exports an object containing both

// app.js (importing)
const addFunction = require('./utils'); // Path to your local file
const { greet } = require('./utils'); // "Cherry-pick" only what you need
console.log(addFunction(5, 10)); // 15
console.log(greet()); // "Hello!"
```
- **No export with default:** You cannot use export default const x = 1; in one line. For a Default Export, you usually declare it first and then export it:
```js
const name = "Meghana";
export default name;

// import { x } is for export const x.
// import x (no braces) is only for export default x

import { PI as MathPI } from './math.js';
```
## Different methods of console such as console.log, console.error, console.info and so on
**console.log():** General purpose logging.
**console.info():** Informational messages (often looks like log but can include a small "i" icon).
**console.warn():** Displays a yellow warning icon. Use this for non-critical issues (like "Deprecated API").
**console.error():** Displays a red error icon and usually includes a Stack Trace. Use this for actual failures.
###  The "Structure" Methods
- console.table(): Displays an array or object as a pretty table
- console.dir(): Shows an interactive list of the properties of a specified JavaScript object (great for inspecting DOM elements).
### The "Grouping" Methods
```js
- console.group("User Data");
- console.log("Name: Meghana");
- console.log("Age: 20");
- console.groupEnd();
```
## The "Utility" Methods
- console.clear(): Clears the console window (keeps it tidy).
- console.count("Label"): Tracks how many times a specific line of code has been executed. Perfect for checking how many times a component renders.
- console.assert(condition, message): Only logs the message if the condition is false. It’s like a mini-test inside your code.

## The "Performance" Methods
```js
console.time("FetchTimer");
// ... some code ...
console.timeEnd("FetchTimer"); // Output: FetchTimer: 15.4ms
```
## All the best practices mentioned on the LMS - indendation, variable naming, loop variable naming and all the others
**1. Indentation & Formatting**

**Consistency is Key:**
Use either 2 spaces or 4 spaces for indentation. Never mix them.

**Space Around Operators:** Use spaces around =, +, -, *, / to make expressions readable.
let x=5+10; ❌
let x = 5 + 10; ✅

**Curly Brace Placement:** Use the "One True Brace Style" (opening brace on the same line).

**2. Variable Naming**

**CamelCase:** In JavaScript, variables and functions always use camelCase.
- user_name ❌ (Snake Case is for Python)
- userName ✅

**Descriptive Names:** Avoid single letters like x, y, or data. Use names that explain what the value is.
- const d = 30; ❌
- const daysUntilExpiration = 30; ✅

**Boolean Naming:** Prefix booleans with is, has, or can.
- const active = true; ❌
- const isActive = true; ✅

**3. Loop Variable Naming**
```js
const users = ["Alice", "Bob"];
users.forEach(user => { // Singular 'user' from plural 'users'
  console.log(user);
});
```
**4. Best Practices for Logic**

**Avoid Magic Numbers:** Don't use raw numbers in your logic. Assign them to a const with a name.
- if (age > 18) ❌
- const LEGAL_AGE = 18; if (age > LEGAL_AGE) ✅

**Dry Principle (Don't Repeat Yourself):**
If you find yourself copy-pasting the same 3 lines of code, move them into a reusable function.

**Use const by Default:** Only use let if you are certain the value will change (like a counter). Never use var.

## Passing functions to other functions and invoking them on demand
-  When you pass a function into another function as an argument, it is called a **Callback Function.**
```js
const numbers = [1, 2, 3, 4, 5];

// A generic "filter" function
function filterArray(arr, conditionFunc) {
  const result = [];
  for (const item of arr) {
    // Invoke the condition function on-demand
    if (conditionFunc(item)) {
      result.push(item);
    }
  }
  return result;
}

// Pass different "logic" functions
const evens = filterArray(numbers, n => n % 2 === 0);
const bigNums = filterArray(numbers, n => n > 3);

console.log(evens);   // [2, 4]
console.log(bigNums); // [4, 5]
```
## Differences between named functions and anonymous functions
```js
// Full Hoisting: Calling before declaration works
sayHello(); 
function sayHello() {
  console.log("Hello!");
}

// ReferenceError: Cannot access 'greet' before initialization
// greet(); 
const greet = function() {
  console.log("Hi there!");
};
```
## Variable number of arguments passed to functions
- In JavaScript, functions are flexible and do not check the number of arguments received. 
- You can handle a variable number of arguments using two primary methods: Rest Parameters (the modern standard) and the arguments object (the legacy approach).
1. Rest Parameters (Modern Standard)
```js
function sum(...numbers) {
  // 'numbers' is a real array
  return numbers.reduce((total, num) => total + num, 0);
}
console.log(sum(1, 2, 3)); // 6
console.log(sum(10, 20));   // 30
```
2. The arguments Object (Legacy)
- doesnot support arrow functions and HOF like map(), filter(), etc
```js
function showArgs() {
  for (let i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}
showArgs("A", "B", "C");
```
## Debugging strategies
**1. Strategic Console Logging**

**console.table():** Use this for arrays of objects to see data in a clean, sortable table format.

**console.assert(condition, message):** Use this to catch "impossible" states. It only logs the message if the condition is false.

**console.trace():** Call this inside a function to see the full Call Stack (the sequence of function calls) that led to that moment.

**Label Your Logs:** Instead of console.log(data), use console.log('User Data:', data) so you don't get lost in a sea of unlabeled values

**2. Core Systematic Strategies**

**Confirm Assumptions:** Many bugs occur because you assume a variable has a certain value or type when it doesn't. Check both the value and the data type (e.g., 5 vs "5").

**Reproduce Consistently:** Before fixing a bug, identify the exact conditions required to make it happen every time.

**Rubber Duck Debugging:** Explain your code line-by-line to an inanimate object (like a rubber duck). Articulating the logic out loud often reveals gaps in your own understanding.

**Isolate the Issue:** Reduce the problem to the smallest possible piece of code. Test that section independently in the console

**3. Technical Debugging Tools**

**The debugger Statement:** Place debugger; directly in your code. If the browser's developer tools are open, it will automatically pause execution at that line so you can inspect the state.

**Breakpoints:** In the Sources tab of DevTools, click a line number to set a breakpoint.
- **Conditional Breakpoints:** Right-click a line number to set a breakpoint that only triggers if a specific condition (e.g., user.id === null) is true.
- **Logpoints:** Add a "logpoint" to print messages to the console without pausing the code or adding console.log to your source files.

**Step-by-Step Execution:** Once paused at a breakpoint, use the controls to:
- **Step Over (F10):** Move to the next line in the current function.
- **Step Into (F11):** Enter the next function call to see its internal logic.
- **Step Out (Shift+F11):** Finish the current function and return to the caller.
