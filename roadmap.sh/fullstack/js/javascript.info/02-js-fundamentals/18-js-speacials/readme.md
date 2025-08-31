

## 🔹 JavaScript Specials (Summary)

### 📌 Code Structure

* Statements usually end with `;` (semicolon).
* Line breaks can also act as statement delimiters (automatic semicolon insertion).
* **Exceptions**:

  ```js
  alert("error here")
  [1,2].forEach(alert) // treated as one line → error
  ```
* No semicolons needed after code blocks `{...}` (functions, loops).
* Extra semicolons are ignored.

<br>

### 📌 Strict Mode

* Enable with:

  ```js
  "use strict";
  ```
* Must be at top of script/function.
* Modern features (e.g., `class`) enable it automatically.
* Without it → old behavior; with it → safer, modern behavior.

<br>

### 📌 Variables

* Declared with `let`, `const`, `var` (old).
* Valid names → letters, digits (not first), `_`, `$`.
* Can store any type (dynamically typed).
* **8 data types**:

  * number
  * bigint
  * string
  * boolean
  * null
  * undefined
  * object
  * symbol
* <mark>`typeof` operator → returns type (with quirks: `typeof null === "object"`, `typeof function(){} === "function"`).</mark>

<br>

### 📌 Interaction (Browser)

* `alert(msg)` → shows a message.
* `prompt(question, [default])` → asks input, returns string or `null`.
* `confirm(question)` → returns `true/false`.
* These are **modal** (pause execution).

<br>

### 📌 Operators

* **Arithmetic**: `+ - * / % **`

  * `+` concatenates strings if any operand is string.
* **Assignment**: `=`, `+=`, `*=`, etc.
* **Bitwise**: `& | ^ ~ << >>` (work on 32-bit ints).
* **Conditional (ternary)**: `cond ? a : b`.
* **Logical**: `&&`, `||`, `!` (short-circuit).
* **Nullish coalescing**: `a ?? b` → `a` if defined, else `b`.
* **Comparisons**:

  * `==` allows type conversion (loose equality).
  * `===` strict (no conversion).
  * `null == undefined` → true, but not equal to anything else.
  * <mark>Strings compared lexicographically.</mark>
    - eg: `'a'>'b' === true`

<br>

### 📌 Loops

* **while**:

  ```js
  while (condition) { ... }
  ```
* **do..while**:

  ```js
  do { ... } while (condition);
  ```
* **for**:

  ```js
  for (let i = 0; i < 10; i++) { ... }
  ```
* Variables in `for(let..)` are block-scoped.
* `break` → exit loop.
* `continue` → skip current iteration.
* Labels can break nested loops.

<br>

### 📌 Switch

* Replaces multiple `if`.
* Uses `===` (strict equality).
* Example:

  ```js
  switch(age) {
    case "18": alert("works"); break;
    default: alert("other");
  }
  ```
* Cases can be grouped (fall-through without `break`).

<br>

### 📌 Functions

* **Declaration**:

  ```js
  function sum(a,b) { return a+b; }
  ```
* **Expression**:

  ```js
  let sum = function(a,b){ return a+b; };
  ```
* **Arrow**:

  ```js
  let sum = (a,b) => a+b;
  let sayHi = () => alert("Hi");
  ```
* Parameters can have defaults:

  ```js
  function sum(a=1,b=2){}
  ```
* Always return something (`undefined` if no `return`).
* Local variables → only inside function.

<br>

✅ That’s the **big-picture summary of all specials** you’ve covered so far.