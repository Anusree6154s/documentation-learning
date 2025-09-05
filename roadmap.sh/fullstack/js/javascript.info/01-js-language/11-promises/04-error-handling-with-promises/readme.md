
### 📌 Promise Error Handling Basics

* A rejected promise or an error inside `.then` jumps to the nearest `.catch`.
* `.catch` doesn’t need to be immediately after — it can be at the end of a long chain.
* `.catch` handles both:

  * Explicit rejections (`reject(error)`)
  * Errors thrown inside promise executors or handlers.

<br>

### 📌 Implicit `try...catch`

* Promise executors and handlers are wrapped in an *invisible `try...catch`*.
* If code throws, the promise automatically becomes rejected.

  ```js
  new Promise(() => { throw new Error("Whoops!"); })
    .catch(console.error);
  ```

<br>

### 📌 Rethrowing Errors

* Inside `.catch`, if you:

  * **Handle the error normally** → next `.then` runs.
  * **Throw/reject again** → control passes to the next `.catch`.

<br>

### 📌 Unhandled Rejections

* If there’s no `.catch`, the rejection gets “stuck”.
* Browser (and Node.js) emits an **unhandled rejection event**.

  ```js
  window.addEventListener('unhandledrejection', event => {
    console.error("Unhandled:", event.reason);
  });
  ```
* Best practice: log/report such errors, since they’re usually fatal.

<br>

### 📌 `.then` Error Handler Alternative

* `.then(success, error)` can also catch errors, but `.catch` is cleaner and more readable.

<br>

### 📌 Best Practices

1. Use `.catch` where recovery is possible.
2. Re-throw unknown/unexpected errors.
3. Always have a global `unhandledrejection` listener (or Node.js equivalent).
4. Avoid leaving promise chains without a `.catch`.
