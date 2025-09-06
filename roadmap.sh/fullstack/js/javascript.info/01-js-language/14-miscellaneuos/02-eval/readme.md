
### 🔹 `eval`: Run a Code String

* Syntax:

  ```js
  let result = eval(code);
  ```
* Executes a **string of code** dynamically.
* Returns the **result of the last statement**.

<br>

### 🔹 Examples

```js
let value = eval('1+1');         // 2
let value = eval('let i=0; ++i'); // 1
```

* Code can contain variables, functions, line breaks, etc.

<br>

### 🔹 Lexical Environment

* `eval` executes in the **current scope** (can access and modify outer variables).

  ```js
  let a = 1;
  eval("a = 10");
  alert(a); // 10
  ```

* **Strict mode**:

  * `eval` has its **own scope**.
  * Variables/functions declared inside are **not visible outside**.

<br>

### 🔹 Why “eval is evil”

* Historically used a lot, but **rarely needed now** (modern JS has better alternatives).
* Problems:

  * **Security risks** (arbitrary code execution).
  * **Harder maintenance** (hidden dependencies on outer variables).
  * **Code minifiers** can’t safely rename variables if `eval` is used → worse compression.

<br>

### 🔹 Safer Alternatives

1. **Run in global scope** with `window.eval`:

   ```js
   let x = 1;
   {
     let x = 5;
     window.eval('alert(x)'); // alerts 1 (global x)
   }
   ```
2. **Use `new Function`** (clearer, no local scope access):

   ```js
   let f = new Function('a', 'return a * 2;');
   alert(f(5)); // 10
   ```

<br>

### 🔹 Summary

* `eval(code)` runs code string, returns last statement result.
* Rarely used today.
* Accessing outer variables → bad practice.
* Prefer:

  * `window.eval(code)` (global scope).
  * `new Function(args, code)` with explicit arguments.

<br>

### 🔹 Task: Eval-Calculator

👉 **Goal:** Prompt user for an arithmetic expression and evaluate it.

✅ **Solution:**

```js
let expr = prompt("Enter an arithmetic expression:", "2+3*4");
alert(eval(expr));
```
