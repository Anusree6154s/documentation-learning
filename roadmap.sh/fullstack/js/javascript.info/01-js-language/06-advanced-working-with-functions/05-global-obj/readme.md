

# 📌 Global Object in JavaScript

### 🔹 What it is

* The **global object** provides variables & functions available everywhere.
* Names differ by environment:

  * Browser → `window`
  * Node.js → `global`
  * Standardized name (all environments) → `globalThis`

<br>

### 🔹 Accessing properties

* Global functions & properties can be accessed directly:

  ```js
  alert("Hi") === window.alert("Hi")
  ```
* `var` variables & function declarations (in script, not modules) become properties of the global object.

  ```js
  var gVar = 5;
  console.log(window.gVar); // 5
  ```
* `let` / `const` do **not** become properties.

  ```js
  let gLet = 5;
  console.log(window.gLet); // undefined
  ```

<br>

### 🔹 Setting globals manually

* Can attach values explicitly:

  ```js
  window.currentUser = { name: "John" };
  console.log(window.currentUser.name); // John
  ```

<br>

### 🔹 Best practices

* Avoid unnecessary globals → harder to test/debug.
* Prefer passing variables into functions instead of relying on globals.
* Only use globals for values that are truly needed everywhere.

<br>

### 🔹 Using for polyfills

* Check if a feature exists, else define it:

  ```js
  if (!window.Promise) {
    window.Promise = function(...) { /* polyfill */ };
  }
  ```

<br>

### 🔹 Summary

* Global object = container of built-ins + environment-specific values.
* Use `globalThis` for universal compatibility.
* Old-style names: `window` (browser), `global` (Node.js).
* Minimize globals for clean & future-proof code.
