

## 📌 Polyfills & Transpilers in JavaScript

### 1. Why needed?

* JavaScript is **constantly evolving** with new features.
* Browsers/engines implement features at **different speeds**.
* Developers want to use modern features → but also support **older browsers**.

<br>

### 2. Tools to bridge the gap

* **Transpilers** → handle **syntax / operators**.
* **Polyfills** → handle **missing functions / APIs**.

<br>

### 3. Transpilers

* Software that **converts modern JS → older JS** syntax.
* Example:

  ```js
  // Modern code (not supported in old browsers)
  height = height ?? 100;

  // After transpiler (works everywhere)
  height = (height !== undefined && height !== null) ? height : 100;
  ```
* Run by developers → transpiled code is deployed to server.
* **Babel** = most popular transpiler.
* Build tools like **webpack** can integrate transpilers automatically.

<br>

### 4. Polyfills

* Scripts that **add missing functions** if the browser doesn’t support them.
* Example:

  ```js
  if (!Math.trunc) {
    Math.trunc = function(num) {
      return num < 0 ? Math.ceil(num) : Math.floor(num);
    };
  }
  ```
* Works because JS allows modifying built-in objects.
* Popular library: **core-js** (selectively loads needed polyfills).

<br>

### 5. Summary

✅ Use **transpilers** → when using **modern syntax / operators** (e.g., `??`, `=>`, `class`).
✅ Use **polyfills** → when using **missing functions / APIs** (e.g., `Math.trunc`, `Promise`).
✅ Always check feature support:

* [compat-table (ES6 features)](https://compat-table.github.io/compat-table/es6/)
* [caniuse.com (browser features)](https://caniuse.com/)

💡 Chrome is usually most up-to-date → try it first if demo code fails.
