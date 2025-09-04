
## 🔹 Promise Basics

1. **Analogy**:

   * *Singer* = producing code (takes time, e.g., network request).
   * *Fans* = consuming code (wants the result).
   * *Subscription list* = the Promise object.

2. **Constructor**:

   ```js
   let promise = new Promise(function(resolve, reject) {
     // executor (producing code)
   });
   ```

   * `executor` runs immediately.
   * `resolve(value)` → success.
   * `reject(error)` → failure.

3. **Internal properties**:

   * `state`: `"pending"` → `"fulfilled"` OR `"rejected"`.
   * `result`: `undefined` → `value` OR `error`.

<br>

## 🔹 Rules

4. **Only one outcome**:

   * A promise can settle **once only** (either resolve OR reject).
   * Further calls are ignored.

5. **Arguments**:

   * `resolve` / `reject` take **one argument** (extra ignored).
   * Prefer rejecting with an `Error` object.

6. **Immediate resolution**:

   * `resolve/reject` can be called synchronously too.

<br>

## 🔹 Consuming a Promise

7. **then**

   ```js
   promise.then(
     result => { /* success */ },
     error => { /* error */ }
   );
   ```

8. **catch**

   * Shortcut for errors only:

   ```js
   promise.catch(err => { ... });
   ```

9. **finally**

   * Runs always (success or error).
   * No arguments.
   * Passes result/error through.
   * Used for cleanup.

<br>

## 🔹 Key Features

10. Handlers (`then/catch/finally`) can be added **anytime**.

    * If the promise is already settled, they run immediately.

11. **Multiple subscribers**:

    * `.then` can be called many times → all handlers run.

<br>

## 🔹 Examples

12. **Simple resolve**:

```js
let promise = new Promise(resolve => {
  setTimeout(() => resolve("done!"), 1000);
});
```

13. **Simple reject**:

```js
let promise = new Promise((_, reject) => {
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});
```

14. **loadScript with Promise**:

```js
function loadScript(src) {
  return new Promise((resolve, reject) => {
    let script = document.createElement('script');
    script.src = src;
    script.onload = () => resolve(script);
    script.onerror = () => reject(new Error(`Error loading ${src}`));
    document.head.append(script);
  });
}
```

<br>

## 🔹 Tasks (from the end)

15. **Re-resolve a promise**

```js
let promise = new Promise(resolve => {
  resolve(1);
  setTimeout(() => resolve(2), 1000); // ignored
});
promise.then(alert); // Output: 1
```

16. **Delay with promise**

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

delay(3000).then(() => alert('runs after 3 seconds'));
```

17. **Animated circle with promise**

```js
function showCircle(cx, cy, radius) {
  let div = document.createElement('div');
  div.style.width = div.style.height = 0;
  div.style.left = cx + "px";
  div.style.top = cy + "px";
  div.className = "circle";
  document.body.append(div);

  return new Promise(resolve => {
    setTimeout(() => {
      div.style.width = div.style.height = radius * 2 + "px";
      div.addEventListener('transitionend', () => resolve(div), {once: true});
    });
  });
}

showCircle(150, 150, 100).then(div => {
  div.classList.add('message-ball');
  div.append("Hello, world!");
});
```
