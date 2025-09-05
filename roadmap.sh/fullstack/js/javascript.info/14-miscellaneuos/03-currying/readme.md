

## 🔹 Currying in JavaScript

### 🔸 What is Currying?

* Currying = transforming a function `f(a, b, c)` into `f(a)(b)(c)`.
* It **doesn’t call** the function, only transforms it.
* Helps create **partial functions** by fixing some arguments.

<br>

### 🔸 Basic Example

```js
function curry(f) {
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}

function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

curriedSum(1)(2); // 3
```

* First call stores `a`, returns a new function.
* Second call uses `b`, executes original function.

<br>

### 🔸 Advanced Curry (multi-argument)

```js
function curry(func) {
  return function curried(...args) {
    if (args.length >= func.length) {
      return func.apply(this, args);
    } else {
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  };
}
```

* If enough arguments → run function.
* If not enough → return another wrapper (partial).
* Supports both:

  * Normal call → `curriedSum(1,2,3)`
  * Partial call → `curriedSum(1)(2)(3)` or `curriedSum(1)(2,3)`

<br>

### 🔸 Practical Use Case: Logging

```js
function log(date, importance, message) {
  alert(`[${date.getHours()}:${date.getMinutes()}] [${importance}] ${message}`);
}

log = _.curry(log);
```

* Can still call normally:
  `log(new Date(), "DEBUG", "some debug")`
* Or curried form:
  `log(new Date())("DEBUG")("some debug")`
* Useful for creating **specialized partials**:

  ```js
  let logNow = log(new Date());   // fixes date
  logNow("INFO", "message");

  let debugNow = logNow("DEBUG"); // fixes date + importance
  debugNow("message");
  ```

<br>

### 🔸 Benefits of Currying

* Still allows **normal calls**.
* Enables **partially applied functions** for convenience.
* Great for reusing functions with fixed arguments.
* Makes code more modular and expressive.

<br>

### 🔸 Limitations

* Works only with **fixed-length functions**.
* Doesn’t work well with `...rest` parameters.
* Overuse may reduce readability.

<br>

### 🔸 Summary

* Currying = `f(a, b, c)` → `f(a)(b)(c)`.
* JavaScript implementations usually support **both normal & partial calls**.
* Useful for generating **partials** (e.g., fixed-date loggers).
* Enhances flexibility and modularity in function usage.
