

## 👋 Hello, World! in JavaScript

### 🔹 Running JavaScript

* JS can run in many environments → in this tutorial: **browser**.
* Minimal browser-specific commands (like `alert`) → focus on **core JavaScript**.
* In Node.js → run with:

  ```bash
  node my.js
  ```

<br>

### 🔹 `<script>` Tag

* Use `<script>` to insert JS into HTML.
* Example:

  ```html
  <!DOCTYPE html>
  <html>
  <body>
    <p>Before the script...</p>
    <script>
      alert("Hello, world!");
    </script>
    <p>...After the script.</p>
  </body>
  </html>
  ```
* Code runs automatically when the browser **parses the tag**.

<br>

### 🔹 Old/Obsolete Attributes

* **`type`** → `type="text/javascript"` (required in HTML4, not needed now).

  * Modern use: `type="module"` (for JS modules, advanced).
* **`language`** → was used to indicate script language (irrelevant now).
* **Comment hacks** (`<!-- ... //-- >`) → used in very old browsers (15+ years). Obsolete.

<br>

### 🔹 External Scripts

* Store JS in **separate files** for larger codebases.
* Use `src` attribute:

  ```html
  <script src="script.js"></script>
  ```
* Path options:

  * Relative → `"./script.js"` (same folder).
  * Absolute → `"/js/script.js"`.
  * Full URL →

    ```html
    <script src="https://cdn.com/lib.js"></script>
    ```
* Multiple scripts = multiple tags:

  ```html
  <script src="one.js"></script>
  <script src="two.js"></script>
  ```

<br>

### 🔹 Rules for `src`

* If `src` is used → **ignore inline content**.

  ```html
  <script src="file.js">
    alert(1); <!-- ignored -->
  </script>
  ```
* ✅ Correct way → separate tags:

  ```html
  <script src="file.js"></script>
  <script>
    alert(1);
  </script>
  ```

<br>

### 🔹 Why External Files?

* Cleaner HTML.
* Reuse across multiple pages.
* Browser **caches** script → loads faster next time.

<br>

### ✅ Summary

* Use `<script>` to run JS in browser.
* `type` & `language` attributes are outdated.
* External scripts = best practice for real projects.
* Only **one purpose per `<script>`**: either inline code OR `src`.
