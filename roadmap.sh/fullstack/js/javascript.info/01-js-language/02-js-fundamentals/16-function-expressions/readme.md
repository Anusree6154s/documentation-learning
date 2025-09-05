
## 🔹 Function Declarations vs Function Expressions (JS)

### 1. Function as a Value

* Functions in JavaScript are **special values** (like numbers/strings).
* Can be stored in variables, copied, or passed around.
* Example:

  ```js
  function sayHi() { alert("Hello"); }  // Declaration
  let func = sayHi;  // copy function into another variable
  func(); // Hello
  ```

<br>

### 2. Function Declaration

* Syntax:

  ```js
  function name(params) { ... }
  ```
* **Created before code runs** (hoisted).
* Can be called **before** it appears in the code.
* Scope: visible throughout the block where declared.
* Example:

  ```js
  sayHi("John"); // works

  function sayHi(name) {
    alert(`Hello, ${name}`);
  }
  ```

<br>

### 3. Function Expression

* Syntax:

  ```js
  let name = function(params) { ... };
  ```
* Created **when execution reaches it** (not hoisted).
* Must be defined **before use**.
* Often anonymous (no function name).
* Ends with a `;` (part of assignment, not function).
* Example:

  ```js
  let sayHi = function() {
    alert("Hello");
  };
  sayHi(); // works only after definition
  ```

<br>

### 4. Callbacks

* Functions can be passed as arguments → called later.
* Example:

  ```js
  function ask(question, yes, no) {
    if (confirm(question)) yes();
    else no();
  }

  ask("Do you agree?",
      () => alert("You agreed."),
      () => alert("You canceled.")
  );
  ```
* Such functions = **callbacks**.

<br>

### 5. Differences (Declaration vs Expression)

* **When created**:

  * Declaration → at script start (hoisted).
  * Expression → only when reached in code.
* **Visibility**:

  * Declaration → whole block.
  * Expression → only after assignment.
* **Usage**:

  * Declaration → better readability, flexibility.
  * Expression → needed for conditional or inline use.

<br>

### 6. Conditional Functions

* Declarations **don’t work well inside blocks** (block scope).
* Solution → use Expression:

  ```js
  let welcome;

  if (age < 18) {
    welcome = function() { alert("Hello!"); };
  } else {
    welcome = function() { alert("Greetings!"); };
  }

  welcome();
  ```
* Or shorter with ternary:

  ```js
  let welcome = (age < 18) ?
      () => alert("Hello!") :
      () => alert("Greetings!");
  ```

<br>

### 7. Summary

* ✅ **Functions are values** → can assign, copy, pass.
* ✅ **Declaration** → hoisted, visible in block, good default choice.
* ✅ **Expression** → created at runtime, useful for conditional/inline cases.
* ✅ **Callbacks** → pass functions as arguments to be executed later.
