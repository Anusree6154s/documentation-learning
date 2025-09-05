
## 🔹 Functions are Objects

* In JavaScript, functions are **callable objects** → they can be invoked, but also have properties (like any object).
* You can add custom properties to them.

<br>

## 🔹 Built-in Function Properties

1. **`name`**

   * Holds the function’s name.
   * If anonymous but assigned, JS infers the name from context.
   * Example:

     ```js
     let f = function() {};
     console.log(f.name); // "f"
     ```
   * Some cases (e.g., function inside array) → name is empty.

2. **`length`**

   * Number of declared parameters.
   * Rest parameters (`...args`) are **not counted**.
   * Example:

     ```js
     function f(a, b) {}
     console.log(f.length); // 2
     ```

<br>

## 🔹 Custom Properties

* Functions can carry extra properties.
* Example:

  ```js
  function sayHi() {
    sayHi.counter++;
  }
  sayHi.counter = 0;
  ```
* Useful for storing state (alternative to closures).
* **Difference:** function properties are **not variables inside the function**, just attached to the object.

<br>

## 🔹 Closure vs Function Property

* **Closure** keeps values in hidden variables (not accessible from outside).
* **Function property** exposes values publicly (can be modified externally).
* Use case depends on whether you want privacy.

<br>

## 🔹 Named Function Expression (NFE)

* Syntax:

  ```js
  let sayHi = function func(who) {
    if (!who) func("Guest");
    else alert(`Hello, ${who}`);
  };
  ```
* Special rules:

  * The internal name (`func`) is **only visible inside the function**.
  * Useful for recursion or self-reference.
  * External code cannot access `func`.

👉 Benefit: safer than using the outer variable (which may change or become `null`).

<br>

## 🔹 Libraries Example

* Libraries often define a single function and attach methods:

  * jQuery → `$`
  * Lodash → `_`
  * Example: `_.clone`, `_.map`, etc.

<br>

## 🔹 Tasks

### 1. Counter with `set` and `decrease`

```js
function makeCounter() {
  function counter() {
    return counter.count++;
  }

  counter.count = 0;

  counter.set = (value) => counter.count = value;
  counter.decrease = () => counter.count--;

  return counter;
}

let c = makeCounter();
console.log(c()); // 0
console.log(c()); // 1
c.set(10);
console.log(c()); // 10
c.decrease();
console.log(c()); // 10 (since decrease happens before next call)
```

### 2. Sum with arbitrary brackets

```js
function sum(a) {
  let current = a;

  function f(b) {
    current += b;
    return f;
  }

  f.toString = () => current;

  return f;
}

console.log(sum(1)(2));      // 3
console.log(sum(1)(2)(3));   // 6
console.log(sum(5)(-1)(2));  // 6
```

<br>

✅ **Summary of key points:**

* Functions = callable objects.
* Properties: `name`, `length`, + custom.
* Can use either **closures** or **function properties** for state.
* **NFE** helps with safe recursion.
* Widely used in libraries (single global + attached methods).
