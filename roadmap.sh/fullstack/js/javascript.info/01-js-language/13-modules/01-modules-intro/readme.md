
### 1. What is a Module?

* A **module = one file** (`.js`).
* Use **`export`** to make code available outside.
* Use **`import`** to bring code in.
* Example:

  ```js
  // sayHi.js
  export function sayHi(user) { alert(`Hello, ${user}`); }

  // main.js
  import {sayHi} from './sayHi.js';
  sayHi("John");
  ```

<br>

### 2. Historical Module Systems

* **AMD** → old system (require.js).
* **CommonJS** → Node.js modules (`require`, `module.exports`).
* **UMD** → universal format (AMD + CommonJS).
* ✅ Modern standard (since 2015): ES Modules (`import/export`).

<br>

### 3. Core Features of ES Modules

* Always **`use strict`** by default.
* Each module has its **own scope** (no global leaks).
* Must use `<script type="module">` in browsers.
* Work only via **HTTP(s)**, not `file://` (need a server or live server).

<br>

### 4. Module Evaluation

* A module is **evaluated once only** (cached).
* Multiple imports share the **same exports object**.
* Exports are **live references** (changes are visible across importers).

  ```js
  // admin.js
  export let admin = { name: "John" };

  // 1.js
  import {admin} from './admin.js';
  admin.name = "Pete";

  // 2.js
  import {admin} from './admin.js';
  console.log(admin.name); // "Pete"
  ```

<br>

### 5. Other Module Features

* `import.meta` → gives info about current module (e.g. URL).
* Top-level `this` = **undefined** (not `window`).
* Can configure modules by exporting objects and mutating them.

<br>

### 6. Browser-Specific Behaviors

* **Deferred by default** → modules load in parallel, run after HTML is parsed.
* **Async works on inline modules** → they can run independently.
* **External module scripts**:

  * Fetched once (duplicates ignored).
  * Require **CORS headers** if loaded cross-origin.
* No **bare imports** in browser → must use relative/absolute paths.

  ```js
  import {sayHi} from './sayHi.js'; // ✅
  import {sayHi} from 'sayHi';      // ❌
  ```

<br>

### 7. Compatibility

* Old browsers ignore `<script type="module">`.
* Use `<script nomodule>` for fallback.

<br>

### 8. Build Tools

* In production, modules are often **bundled** (Webpack, Rollup, Parcel).
* Benefits:

  * Tree-shaking (remove unused code).
  * Minification.
  * Transpilation (via Babel).
  * Support for CSS/HTML modules.
* Result: single optimized file, no `import/export` left, just `<script src="bundle.js">`.

<br>

### 9. Summary

* **Module = file**.
* Use `export` / `import`.
* Modules are **strict**, **scoped**, **cached once**, and **shared**.
* Browser requires `<script type="module">`.
* In practice, bundlers are often used for efficiency.
