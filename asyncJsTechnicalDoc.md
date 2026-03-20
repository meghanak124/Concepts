# Asynchronous Javascript

## 1. How JavaScript Executes Code

### Execution Context
Every JavaScript code runs inside an Execution Context.
There are two types:
- Global Execution Context (GEC)
- Function Execution Context (FEC)

### Phases of Execution Context

#### 1. Memory Creation Phase (Hoisting)
- Variables → initialized as undefined
- Functions → whole function code is stored entirely in memory

Example:
```js
console.log(a); // undefined
var a = 10;
```

#### 2. Execution Phase
- Code executes line by line
- Values assigned
- Functions invoked

### Call Stack
- A stack (LIFO) that keeps track of function execution.
- When a function is called → pushed into stack
- When it completes → popped out
```js
function a() {
  console.log("A");
}
function b() {
  a();
}
b();
```
- Call Stack:       b() → a() → print → pop → pop

---

## 2. Synchronous vs Asynchronous JavaScript

### Synchronous
- Executes line-by-line
- Blocking nature
```js
console.log("Start");
console.log("End");
```

### Asynchronous
- Non-blocking
- Allows other operations while waiting
```js
console.log("Start");
setTimeout(() => console.log("Async"), 2000);
console.log("End");
/*Start
End
Async*/
```
---

## 3. Ways to Make Code Asynchronous

- Callbacks
- Promises
- Async/Await
- Web APIs (setTimeout, fetch)
- Event listeners

---

## 4. Web Browser APIs

Provided by browser:
- setTimeout
- fetch
- DOM APIs
- localStorage
- console
- location

They run outside JS engine.

---

## 5. Event Loop

Responsible for handling async operations.

The Event Loop connects:
- Call Stack
- Callback Queue
- Web APIs

Flow:
1. Call Stack executes code
2. Async tasks go to Web APIs
3. Callback queue stores callbacks
4. Event loop pushes them back to stack

---

## 6. Callback Hell

Nested callbacks causing unreadable code.

Problem:
- Hard to debug
- Poor readability
```js
setTimeout(() => {
  console.log("Step 1");
  setTimeout(() => {
    console.log("Step 2");
    setTimeout(() => {
      console.log("Step 3");
    }, 1000);
  }, 1000);
}, 1000);
```

---

## 7. Inversion of Control

You pass control of execution to another function.
Risk:
- May not execute
- May execute multiple times
```js
apiCall(function () {
  // You don't control when/if this runs
});
```
---

## 8. Promises

### What is a Promise?
An object representing eventual completion or rejection of a ashynchronous operation.

### States:
- Pending → initial state
- Fulfilled → success (resolve)
- Rejected → failure (reject)

---

## 9. Creating a Promise

```js
const promise = new Promise((resolve, reject) => {
  if (true) resolve("Success");
  else reject("Error");
});
```

---

## 10. Consuming a Promise

```js
promise
  .then(result => console.log(result))
  .catch(err => console.log(err));
```

---

## 11. Promise Chaining

- .then for chaining
```js
fetchData()
  .then(data => process(data))
  .then(result => console.log(result));
```
- .catch for errors
```js
fetchData()
  .then(data => { throw new Error("Oops"); })
  .catch(err => console.log(err));
```
- .finally always runs
```js
fetchData()
  .finally(() => console.log("Always runs"));
```
  ---

## 12. Error Handling

- Always use .catch
- Place at end
- Prevent unhandled rejections

- Error Inside .then : 

With .catch : Error is caught

Without .catch : Unhandled Promise

- Rejection (runtime error)

Why .catch() at End?
Because:
- It catches errors from all previous .then() blocks

---

## 13. Multiple Promises

```js
task1()
  .then(() => task2())
  .then(() => task3());
```

### Promise.all
- Runs parallel
- Fails if one fails
```js
Promise.all([p1, p2, p3])
  .then(results => console.log(results))
  .catch(err => console.log(err));
```

### Promise.allSettled
- Returns all results
```js
Promise.allSettled([p1, p2]);
```

### Promise.any
- First success
```js
Promise.any([p1, p2]);
```

### Promise.race
- First settled
```js
Promise.race([p1, p2]);
```

---

## 14. Promisification

Convert callbacks to promises.


Example:
```js
function delay(ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms);
  });
}
```
```js
// EXAMPLE
const fs = require("fs");

function readFilePromise(path) {
  return new Promise((resolve, reject) => {
    fs.readFile(path, "utf8", (err, data) => {
      if (err) reject(err);
      else resolve(data);
    });
  });
}
```

---

## 15. Built-in Methods

- Promise.resolve()
```js
Promise.resolve("Success");
```
- Promise.reject()
```js
Promise.reject("Error");
```
- Promise.all()
- Promise.allSettled()
- Promise.any()
- Promise.race()

Promises help manage async code cleanly and avoid callback hell.
