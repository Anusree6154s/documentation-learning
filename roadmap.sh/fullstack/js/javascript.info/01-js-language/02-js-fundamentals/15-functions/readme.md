
## **Functions in JavaScript**

### **Basics**

* Functions let us group code for reuse and clarity.
* Declared with the `function` keyword:

  ```js
  function name(param1, param2, ...) {
    // body
  }
  ```
* Called by name: `showMessage();`

<br>

### **Variables**

* **Local variables**: Declared inside a function, only accessible there.
* **Outer variables**: Functions can read/modify them.
* **Shadowing**: Local variable with the same name hides the outer one.
```js
let userName = "Alice"; // outer (global) variable

function showMessage() {
  let userName = "Bob"; // local variable shadows the outer one
  console.log("Hello, " + userName);
}

showMessage();   // Hello, Bob  (local variable used)
console.log(userName); // Alice (outer variable remains unchanged)

```
* **Global variables**: Declared outside functions, visible everywhere (use sparingly).

<br>

### **Parameters & Arguments**

* Parameters → variables in the declaration.
* Arguments → values passed when calling.
* Functions always work with **copies of values**.

<br>

### **Default Parameters**

* If not provided, parameters = `undefined`.
* Can assign defaults:

  ```js
  function showMessage(text = "no text") { ... }
  ```
* Defaults are re-evaluated each call.
* Old JS: use `if (param === undefined)`, `||`, or `??`.

<br>

### **Return Values**

* `return` sends a value back.
* Without value → `undefined`.
* Ends function execution immediately.
* Don’t place line break right after `return`.

<br>

### **Naming Conventions**

* Should describe **what the function does**.
* Common prefixes:

  * `show...` → display something
  * `get...` → return a value
  * `calc...` → calculate result
  * `create...` → build and return
  * `check...` → return boolean
* One function = one action.
* Avoid mixing unrelated tasks.

<br>

### **Best Practices**

* Use functions to **avoid code duplication**.
* Prefer **local variables and parameters** over globals.
* Functions make code more **readable, testable, and self-describing**.
* Short, single-purpose functions act as **comments** in code.

<br>

✅ Functions are the **main building blocks** of JavaScript.
They improve **clarity, reuse, and structure**.
