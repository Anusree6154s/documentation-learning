

# 📌 Variable Scope & Closures in JavaScript — Key Points

### 1. **Variable Scope**

* `let` and `const` → block scoped (only accessible inside `{ ... }`).
* `var` → function scoped (ignores blocks like `if`, `for`).
* Functions create their own scope.

### 2. **Nested Functions**

* Functions can be created inside other functions.
* Inner functions can access variables from outer functions.

### 3. **Lexical Environment**

* Each block/function/script has a hidden object storing variables.
* A variable lookup:

  * Starts from inner scope → outer scope → global.
* Functions carry a hidden property `[[Environment]]` which remembers where they were created.

### 4. **Closures**

* A closure = function + its surrounding lexical environment.
* All JS functions are closures (except those created with `new Function`).
* Closure allows a function to "remember" outer variables even after the outer function has finished.

### 5. **Garbage Collection**

* Normally, local variables are deleted when a function ends.
* BUT if an inner function still references them, they remain in memory.
* Once no function references them, they are cleared.

<br>

# 📌 Task Solutions (Short & Clear)

### ✅ Task 1: Does function pick up latest changes?

```js
let name = "John";
function sayHi() {
  alert("Hi, " + name);
}
name = "Pete";
sayHi(); // "Hi, Pete"
```

👉 Always uses **latest value**, because it looks up variables when called.

<br>

### ✅ Task 2: Which variables are available?

```js
function makeWorker() {
  let name = "Pete";
  return function() { alert(name); };
}
let name = "John";
let work = makeWorker();
work(); // "Pete"
```

👉 Function remembers **creation environment**, not where it’s called.

<br>

### ✅ Task 3: Are counters independent?

```js
let counter = makeCounter();
let counter2 = makeCounter();

alert(counter());  // 0
alert(counter());  // 1
alert(counter2()); // 0
alert(counter2()); // 1
```

👉 Each call to `makeCounter()` creates a **new independent closure**.

<br>

### ✅ Task 4: Counter object

```js
function Counter() {
  let count = 0;
  this.up = () => ++count;
  this.down = () => --count;
}
let counter = new Counter();

alert(counter.up());   // 1
alert(counter.up());   // 2
alert(counter.down()); // 1
```

👉 Works fine, both methods share the same closure over `count`.

<br>

### ✅ Task 5: Function in if

```js
let phrase = "Hello";
if (true) {
  let user = "John";
  function sayHi() {
    alert(`${phrase}, ${user}`);
  }
}
sayHi(); // Error in strict mode
```

👉 Function inside `if` is block-scoped → **not visible outside**.

<br>

### ✅ Task 6: Sum with closures

```js
function sum(a) {
  return function(b) {
    return a + b;
  }
}

sum(1)(2);   // 3
sum(5)(-1);  // 4
```

👉 Uses closures to "remember" first argument.

<br>

### ✅ Task 7: Is variable visible?

```js
let x = 1;
function func() {
  console.log(x); // ReferenceError
  let x = 2;
}
func();
```

👉 `let x` is hoisted but uninitialized → **Temporal Dead Zone** error.

<br>

### ✅ Task 8: Filter through function

```js
function inBetween(a, b) {
  return function(x) {
    return x >= a && x <= b;
  };
}
function inArray(arr) {
  return function(x) {
    return arr.includes(x);
  };
}

let arr = [1,2,3,4,5,6,7];
arr.filter(inBetween(3,6)); // 3,4,5,6
arr.filter(inArray([1,2,10])); // 1,2
```

<br>

### ✅ Task 9: Sort by field

```js
function byField(field) {
  return (a, b) => a[field] > b[field] ? 1 : -1;
}

users.sort(byField('name')); // Ann, John, Pete
users.sort(byField('age'));  // Pete, Ann, John
```

<br>

### ✅ Task 10: Army of functions (fix)

```js
function makeArmy() {
  let shooters = [];
  for (let i = 0; i < 10; i++) {
    let shooter = function() {
      alert(i);
    };
    shooters.push(shooter);
  }
  return shooters;
}

let army = makeArmy();
army[0](); // 0
army[1](); // 1
army[2](); // 2
```

👉 Using `let i` inside loop creates a new binding per iteration.

<br>

# 🎯 TL;DR

* **Closures = function + remembered environment**.
* Functions always use the **current value of variables at call time**.
* Each function call creates a new independent lexical environment.
* Block-scoped variables (`let`, `const`) are safe, while `var` has quirks.
