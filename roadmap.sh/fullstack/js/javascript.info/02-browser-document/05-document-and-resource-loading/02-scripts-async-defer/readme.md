
## 📜 Scripts: `async` vs `defer`

### 1. The Problem with Regular Scripts

* `<script>` blocks HTML parsing: browser stops, downloads, executes, then continues.
* Issues:

  * Scripts can’t “see” elements below them.
  * Page content blocked until script loads.
* Workaround: put scripts at bottom → but downloading starts only after full HTML is loaded (still a delay).

<br>

### 2. `defer`

* Loads script **in background** while HTML is being parsed.
* Executes **after DOM is fully built**, before `DOMContentLoaded`.
* ✅ Advantages:

  * Doesn’t block page rendering.
  * Runs **in document order** (guaranteed).
  * Good for libraries + dependent scripts.
* ⚠️ Only works with **external scripts** (`src`).

<br>

### 3. `async`

* Loads script **in background**, executes immediately when ready.
* Independent:

  * Doesn’t block HTML parsing.
  * Doesn’t wait for other scripts.
  * Others don’t wait for it.
* Runs in **load-first order** (whichever finishes first runs first).
* `DOMContentLoaded` timing is unaffected (may happen before or after async).
* ✅ Best for independent third-party scripts (ads, analytics, counters).
* ⚠️ Only works with **external scripts** (`src`).

<br>

### 4. Dynamic Scripts

* Can create scripts via JS:

  ```js
  let script = document.createElement('script');
  script.src = "file.js";
  document.body.append(script);
  ```
* By default → behaves like **async** (load-first order).
* To make it behave like **defer**, set `script.async = false` before appending.

<br>

### 5. Comparison: `async` vs `defer`

| Feature            | `async` 🚀                           | `defer` ⏳                                   |
| ------------------ | ------------------------------------ | ------------------------------------------- |
| Execution order    | Load-first (random)                  | Document order                              |
| `DOMContentLoaded` | Doesn’t wait                         | Waits for all defer scripts                 |
| Use case           | Independent scripts (ads, analytics) | Scripts that depend on DOM or other scripts |

<br>

### 6. Best Practices

* Use **`defer`** for main scripts that need DOM or depend on each other.
* Use **`async`** for third-party/independent scripts.
* Page should remain usable before scripts finish loading → add loading indicators, disable unready features.
