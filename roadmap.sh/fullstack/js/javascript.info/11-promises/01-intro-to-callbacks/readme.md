

### 🔹 Introduction to Callbacks
- Many JavaScript actions are **asynchronous** (start now, finish later).
- Example: `setTimeout`, loading scripts, fetching data.
- To handle results after an async task finishes, we use **callbacks**.

<br>

### 🔹 Example: `loadScript(src)`
- Creates and appends a `<script>` tag dynamically → browser loads and executes it.
- Code below `loadScript()` does **not wait** for the script to load.
- If you try to use functions from the script immediately → **error**, since it may not have loaded yet.

<br>

### 🔹 Adding a Callback
- Pass a function (`callback`) to run after the script loads:
  ```js
  function loadScript(src, callback) {
    let script = document.createElement('script');
    script.src = src;
    script.onload = () => callback(script);
    document.head.append(script);
  }
  ```
- Usage:
  ```js
  loadScript('/my/script.js', () => {
    newFunction(); // works now
  });
  ```

<br>

### 🔹 Callback in Callback (Sequential Loading)
- To load multiple scripts **in order**:
  ```js
  loadScript('1.js', () => {
    loadScript('2.js', () => {
      loadScript('3.js', () => {
        // continue...
      });
    });
  });
  ```
- This creates **nested callbacks**.

<br>

### 🔹 Handling Errors (Error-First Callback)
- Improved version with error handling:
  ```js
  function loadScript(src, callback) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => callback(null, script);
    script.onerror = () => callback(new Error(`Failed to load ${src}`));

    document.head.append(script);
  }
  ```
- Convention:
  - `callback(error, result)`
  - `error` is `null` if successful.
  - `result` contains the data/script/etc.

<br>

### 🔹 Pyramid of Doom (Callback Hell)
- Multiple nested async calls → deeply indented code.
- Hard to read, debug, and maintain.
- Example:
  ```js
  loadScript('1.js', (err, script) => {
    if (!err) {
      loadScript('2.js', (err, script) => {
        if (!err) {
          loadScript('3.js', (err, script) => {
            if (!err) {
              // final code
            }
          });
        }
      });
    }
  });
  ```

<br>

### 🔹 Workarounds
- Break into separate functions:
  ```js
  loadScript('1.js', step1);

  function step1(err, script) {
    if (!err) loadScript('2.js', step2);
  }
  function step2(err, script) {
    if (!err) loadScript('3.js', step3);
  }
  function step3(err, script) {
    if (!err) { /* continue */ }
  }
  ```
- Avoids nesting but leads to:
  - Scattered code.
  - Single-use helper functions cluttering namespace.

<br>

### 🔹 Conclusion
- Callbacks allow handling async results.
- Problems:
  - Callback hell / Pyramid of Doom.
  - Hard-to-read, hard-to-maintain code.
- **Better solution → Promises** (covered in next chapter).
