
# 🌐 Page Lifecycle Events in JavaScript

### 🔹 Main Events

* **DOMContentLoaded (document)**

  * Fires when **DOM is fully built**.
  * External resources (images, CSS) may still be loading.
  * Best for running scripts that need the DOM ready.

* **load (window)**

  * Fires when **all resources (HTML, CSS, images, iframes, etc.)** are loaded.
  * Useful when you need final sizes, styles, or image dimensions.

* **beforeunload (window)**

  * Fires when user **tries to leave/reload/close page**.
  * Can cancel event → browser asks for confirmation (e.g. “Unsaved changes?”).
  * Use by setting `event.returnValue = "message"` (not `preventDefault()`).

* **unload (window)**

  * Fires when user **is leaving the page**.
  * Only simple, non-blocking tasks allowed.
  * Use `navigator.sendBeacon()` for analytics or cleanup requests.

<br>

### 🔹 DOMContentLoaded Details

* Triggered on `document`. Must use `addEventListener`.
* Scripts **block** DOMContentLoaded (browser waits for them to run).
* Exceptions (don’t block):

  * `<script async>`
  * Dynamically created `<script>` via `createElement`.
* Stylesheets alone don’t block, but **scripts after styles** wait for them to load.
* Autofill (Chrome/Firefox/Opera) usually happens on DOMContentLoaded.

<br>

### 🔹 window\.onload

* Fires only when everything is loaded.
* Example: checking image dimensions works here, not in DOMContentLoaded.

<br>

### 🔹 window\.onbeforeunload

* Lets you warn user before leaving.
* Example:

  ```js
  window.onbeforeunload = function() {
    return "Unsaved changes. Leave?";
  };
  ```
* `event.preventDefault()` is ignored. Must use `event.returnValue`.
* Modern browsers don’t allow custom text messages (show generic warning instead).

<br>

### 🔹 window\.onunload

* Final stage → page is closing.
* Can’t cancel navigation here.
* Use for lightweight async cleanup:

  ```js
  window.addEventListener("unload", () => {
    navigator.sendBeacon("/analytics", JSON.stringify(data));
  });
  ```

<br>

### 🔹 document.readyState

* Possible values:

  * `"loading"` → document is still loading.
  * `"interactive"` → DOM is parsed (≈ DOMContentLoaded).
  * `"complete"` → all resources loaded (≈ window\.onload).
* Can run code immediately if already ready:

  ```js
  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", work);
  } else {
    work();
  }
  ```
* `readystatechange` event → fires on state changes.

<br>

### 🔹 Event Order Example

1. `readyState: loading`
2. `readyState: interactive` → `DOMContentLoaded`
3. `<iframe>.onload`
4. `<img>.onload` → `readyState: complete` → `window.onload`

<br>

### ✅ Summary

* **DOMContentLoaded** → DOM ready (best for most scripts).
* **load** → everything loaded (rarely needed).
* **beforeunload** → confirm before leaving.
* **unload** → final cleanup, send analytics.
* **readyState** → allows checking load status at any time.
