
## 🔹 Debugging in the Browser (Chrome DevTools)

### 1. What is Debugging?

* Process of **finding and fixing errors** in scripts.
* Tools allow stepping through code, checking variables, and understanding execution flow.

<br>

### 2. The **Sources Panel**

* Open DevTools → **F12** (Windows/Linux) or **Cmd+Opt+I** (Mac).
* Go to **Sources tab** → shows 3 parts:

  1. **File Navigator** → lists all files (HTML, JS, CSS, images, extensions).
  2. **Code Editor** → shows source code.
  3. **Debugging Pane** → breakpoints, call stack, scope, watches.
* Press **Esc** → console opens at bottom (run JS commands).

<br>

### 3. Breakpoints

* **Set breakpoint** → click line number in code.
* Execution **pauses** there.
* Manage breakpoints in right panel:

  * Disable temporarily (uncheck).
  * Remove (right click → remove).

✅ **Conditional breakpoints** → right-click line → set condition (runs only if expression is truthy).

<br>

### 4. The `debugger` Statement

* Add inside code to pause execution:

  ```js
  function hello(name) {
    let phrase = `Hello, ${name}!`;
    debugger; // pauses here if DevTools open
    console.log(phrase);
  }
  ```

<br>

### 5. Debugger Information Panels

* **Watch** → track values of expressions.
* **Call Stack** → shows chain of nested function calls.
* **Scope** → inspect variables:

  * Local (inside function).
  * Global (outside functions).
  * `this` keyword also visible.

<br>

### 6. Execution Controls (Top Right Buttons)

* ▶ **Resume (F8)** → continue until next breakpoint.
* ⬇ **Step (F9)** → run next statement (go inside function).
* ↷ **Step over (F10)** → run function call without entering.
* ⤴ **Step into (F11)** → like Step, but also handles async calls.
* ⬆ **Step out (Shift+F11)** → finish current function, pause after.
* ⭕ Toggle breakpoints on/off.
* ⚠ Pause on errors → automatically stop when error occurs.

<br>

### 7. Extra Features

* **Continue to here** → right click line → run until that line.
* **Logging with console.log** → send messages to console:

  ```js
  for (let i = 0; i < 5; i++) {
    console.log("value:", i);
  }
  ```

<br>

### 8. Summary

* ✅ **Ways to pause script**:

  1. Breakpoints.
  2. `debugger` statement.
  3. Errors (with DevTools open & pause-on-errors enabled).

* ✅ Debugging lets you:

  * Inspect variables.
  * Step through code execution.
  * Find where logic goes wrong.

* ✅ **Console logging** = quick way to debug without pausing.
