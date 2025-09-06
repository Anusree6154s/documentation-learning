
## 🔹 Resource Loading Events

* Two key events for external resources (`<script>`, `<img>`, `<iframe>`, etc.):

  * **`onload`** → fires when resource **successfully loads & executes**.
  * **`onerror`** → fires when resource **fails to load** (404, offline, etc.).

---

## 🔹 Scripts

* Scripts can be loaded dynamically:

  ```js
  let script = document.createElement('script');
  script.src = "my.js";
  document.head.append(script);
  ```
* **`script.onload`** → fires after script loads & executes → safe to use its functions/variables.
* **`script.onerror`** → fires if loading fails (e.g., 404).

  * Does **not** provide HTTP error details (only “failed”).
* Important: `onload/onerror` only track **loading**, not runtime errors.

  * Runtime errors must be caught with `window.onerror`.

---

## 🔹 Other Resources

* Works similarly for `<img>`, `<link>`, etc.

  ```js
  let img = document.createElement('img');
  img.src = "pic.png";
  img.onload = () => alert("Loaded");
  img.onerror = () => alert("Error");
  ```
* `<img>` loads only when `src` is set.
* `<iframe>` → `onload` fires **always** (success or error), due to legacy behavior.

---

## 🔹 Cross-Origin Restrictions (CORS)

* Scripts from another **origin** (domain/port/protocol) cannot expose detailed errors.

  * Example: `window.onerror` only reports `"Script error."` for cross-origin scripts.
* To allow error reporting, use `crossorigin` attribute **and** server must send headers:

  * `crossorigin="anonymous"` → allows access if server sends `Access-Control-Allow-Origin`.
  * `crossorigin="use-credentials"` → also sends cookies, requires extra header `Access-Control-Allow-Credentials: true`.
* Without proper setup → only `"Script error."`, no stack trace.

---

## 🔹 Summary

* `load` → fires when resource successfully loads.
* `error` → fires when resource fails to load.
* `<iframe>` → always fires `load`, even on error.
* Cross-origin scripts need `crossorigin` + server headers for full error reports.

---

## 🔹 Task: Preload Images

👉 Goal: Load multiple images first, then run a callback when **all are either loaded or errored**.

**Solution outline:**

```js
function preloadImages(sources, callback) {
  let loadedCount = 0;

  function checkDone() {
    loadedCount++;
    if (loadedCount === sources.length) callback();
  }

  for (let src of sources) {
    let img = document.createElement('img');
    img.src = src;

    img.onload = checkDone;
    img.onerror = checkDone; // error still counts as "done"
  }
}

// Usage:
preloadImages(["1.jpg", "2.jpg", "3.jpg"], () => {
  alert("Images loaded");
});
```
