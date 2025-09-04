
### 1. What is Promisification?

* Converting a **callback-based function** into a function that **returns a Promise**.
* Useful because many old libraries use callbacks, but promises (and `async/await`) are easier to work with.

<br>

### 2. Example: `loadScript`

Callback-based:

```js
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`Script load error for ${src}`));

  document.head.append(script);
}
```

Promisified version:

```js
function loadScriptPromise(src) {
  return new Promise((resolve, reject) => {
    loadScript(src, (err, script) => {
      if (err) reject(err);
      else resolve(script);
    });
  });
}
```

<br>

### 3. Generic `promisify(f)` Helper

```js
function promisify(f) {
  return function (...args) {
    return new Promise((resolve, reject) => {
      function callback(err, result) {
        if (err) reject(err);
        else resolve(result);
      }
      args.push(callback);
      f.call(this, ...args);
    });
  };
}
```

* Wraps any callback-style function `f(err, result)` into a promise-returning one.

Usage:

```js
let loadScriptPromise = promisify(loadScript);
loadScriptPromise('file.js').then(...).catch(...);
```

<br>

### 4. Advanced `promisify` (multiple callback results)

```js
function promisify(f, manyArgs = false) {
  return function (...args) {
    return new Promise((resolve, reject) => {
      function callback(err, ...results) {
        if (err) reject(err);
        else resolve(manyArgs ? results : results[0]);
      }
      args.push(callback);
      f.call(this, ...args);
    });
  };
}
```

* `promisify(f)` → resolves with **first callback result**.
* `promisify(f, true)` → resolves with **array of all results**.

<br>

### 5. Limitations

* Works only if the callback is called **once**.

  * Promises can resolve/reject only once.
  * If a callback-based API calls back multiple times (like event listeners), promisification is not suitable.
* For unusual callback formats (e.g., no `err` parameter), manual promisification is needed.

<br>

### 6. Existing Helpers

* **Node.js** has built-in `util.promisify`.
* External packages: e.g. `es6-promisify`.

<br>

✅ **Summary:**
Promisification is wrapping callback-based functions so they return promises. It simplifies code, works great with `async/await`, and is widely used in modern JavaScript.
