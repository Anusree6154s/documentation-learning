
## 🔹 AbortController Basics

* Special built-in object to **abort async operations** (e.g., `fetch`).
* Usage:

  ```js
  let controller = new AbortController();
  let signal = controller.signal;
  ```
* Properties & methods:

  * `controller.abort()` → triggers abort.
  * `signal` → object that:

    * emits `"abort"` event.
    * has property `aborted = true` after abort.

<br>

## 🔹 How It Works

* **Two parties:**

  1. **Cancelable task** → listens to `signal`.
  2. **Controller** → calls `abort()` when cancel needed.
* Example:

  ```js
  signal.addEventListener('abort', () => alert("aborted!"));
  controller.abort(); // triggers event
  ```

<br>

## 🔹 Using with fetch

* Pass `signal` to `fetch`:

  ```js
  let controller = new AbortController();
  fetch(url, { signal: controller.signal });
  ```
* Calling `controller.abort()` → cancels fetch.
* When aborted → `fetch` rejects with `AbortError`.
* Example:

  ```js
  try {
    let response = await fetch(url, { signal: controller.signal });
  } catch (err) {
    if (err.name === 'AbortError') {
      console.log("Request aborted");
    } else {
      throw err;
    }
  }
  ```

<br>

## 🔹 Aborting After Timeout

```js
let controller = new AbortController();
setTimeout(() => controller.abort(), 1000); // abort after 1s
```

<br>

## 🔹 Aborting Multiple Fetches

* One controller can manage **many fetch requests**:

  ```js
  let urls = [...];
  let controller = new AbortController();

  let jobs = urls.map(url => fetch(url, { signal: controller.signal }));

  // calling controller.abort() cancels all
  ```

<br>

## 🔹 Aborting Custom Async Tasks

* Works with **custom promises** too:

  ```js
  let job = new Promise((res, rej) => {
    controller.signal.addEventListener('abort', () => rej("Aborted"));
  });
  ```
* Same controller can cancel **fetches + custom tasks** together.

<br>

## ✅ Summary

* `AbortController` = simple way to signal cancellation.
* `abort()` → sets `signal.aborted = true` and dispatches `"abort"`.
* `fetch` natively supports it (via `signal` option).
* Can control multiple fetches or custom async tasks with one controller.
