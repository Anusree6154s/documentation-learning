
## 🔹 Key Concepts

1. **Decorator** = A wrapper around a function that alters or extends its behavior without modifying its original code.

   ```js
   function wrapper(...args) {
     // do something before/after
     return original(...args);
   }
   ```

2. **Benefits of decorators:**

   * Reusable across multiple functions.
   * Keeps core function simple.
   * Multiple decorators can be combined.

<br>

## 🔹 Context Problem (`this`)

* If you decorate an **object method**, you must preserve its `this`.
* Direct call like `func(x)` loses the `this` context.
* Fix: use `.call` or `.apply`.

```js
func.call(this, ...args); 
func.apply(this, args);
```

<br>

## 🔹 Call vs Apply

* **`func.call(context, arg1, arg2, ...)`** → Pass args one by one.
* **`func.apply(context, argsArray)`** → Pass args as an array/array-like.
* Both set the context (`this`) explicitly.

<br>

## 🔹 Call Forwarding

Forwarding all arguments + context:

```js
let wrapper = function(...args) {
  return func.apply(this, args);
};
```

<br>

## 🔹 Method Borrowing

* `arguments` is **array-like** but not a real array.
* Borrow array methods using `.call`:

```js
[].join.call(arguments) // works
```

<br>

## 🔹 Task Solutions

### 1. ✅ Spy Decorator

Tracks calls & arguments.

```js
function spy(func) {
  function wrapper(...args) {
    wrapper.calls.push(args);
    return func.apply(this, args);
  }
  wrapper.calls = [];
  return wrapper;
}
```

<br>

### 2. ✅ Delay Decorator

Runs function after `ms`.

```js
function delay(func, ms) {
  return function(...args) {
    setTimeout(() => func.apply(this, args), ms);
  };
}
```

<br>

### 3. ✅ Debounce Decorator

Waits until no calls for `ms`, then executes **last call only**.

```js
function debounce(func, ms) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(this, args), ms);
  };
}
```

<br>

### 4. ✅ Throttle Decorator

Runs immediately, then at most once every `ms`, and runs **last call** after cooldown.

```js
function throttle(func, ms) {
  let isThrottled = false,
      savedArgs,
      savedThis;

  function wrapper(...args) {
    if (isThrottled) {
      savedArgs = args;
      savedThis = this;
      return;
    }

    func.apply(this, args);
    isThrottled = true;

    setTimeout(() => {
      isThrottled = false;
      if (savedArgs) {
        wrapper.apply(savedThis, savedArgs);
        savedArgs = savedThis = null;
      }
    }, ms);
  }

  return wrapper;
}
```

<br>

## 🔹 Summary

* **Decorator = wrapper** → modifies behavior.
* Use `.call`/`.apply` to preserve `this` & arguments.
* `spy`, `delay`, `debounce`, `throttle` are classic decorators.
* **Spy** → logs calls.
* **Delay** → delays execution.
* **Debounce** → executes after inactivity.
* **Throttle** → executes at most once per interval.
