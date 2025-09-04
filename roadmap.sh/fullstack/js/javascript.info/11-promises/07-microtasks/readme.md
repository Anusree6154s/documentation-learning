

### 🔹 Promise Handlers Are Always Asynchronous

* `.then`, `.catch`, `.finally` **never run immediately**.
* Even if a promise is already resolved, the code below runs first.

  ```js
  let promise = Promise.resolve();
  promise.then(() => alert("promise done!"));
  alert("code finished"); // runs first
  ```

<br>

### 🔹 Why? → Microtasks Queue

* JavaScript uses an internal **queue** for async tasks → called **PromiseJobs** or **microtask queue**.
* Rules:

  * **FIFO** (first-in, first-out).
  * Tasks run **only when current code finishes**.
* Promise handlers are **queued first**, then executed after synchronous code.

<br>

### 🔹 Multiple `.then` Handlers

* Each `.then` / `.catch` / `.finally` is **queued separately**.
* Execution order:

  1. Run current synchronous code.
  2. Process queued handlers one by one.
* Example to enforce order:

  ```js
  Promise.resolve()
    .then(() => alert("promise done!"))
    .then(() => alert("code finished"));
  ```

<br>

### 🔹 Unhandled Rejections

* If a promise is rejected without `.catch`, after the microtask queue is empty → `unhandledrejection` event fires.

  ```js
  let promise = Promise.reject(new Error("Failed!"));
  window.addEventListener('unhandledrejection', e => alert(e.reason));
  ```
* If `.catch` exists → error handled, event doesn’t fire.

<br>

### 🔹 Late Error Handling

* If `.catch` is added later (e.g., inside `setTimeout`) → too late.
* Engine already emitted `unhandledrejection`.
* Example:

  ```js
  let promise = Promise.reject(new Error("Failed!"));
  setTimeout(() => promise.catch(err => alert("caught")), 1000);
  ```

  Output:

  * First: `"Failed!"` from `unhandledrejection`.
  * Then: `"caught"` from delayed `.catch`.

<br>

### 🔹 Summary

* Promise handling is always **asynchronous** via the **microtask queue**.
* `.then`, `.catch`, `.finally` → run **after current code completes**.
* To guarantee order → chain `.then`.
* `unhandledrejection` triggers if a rejected promise has **no `.catch`** by the end of the microtask queue.
* Microtasks are part of the **event loop** (connected with macrotasks, covered later).
