

### 🔹 Basics of `try...catch`

* JavaScript normally stops execution (script “dies”) when an error occurs.
* `try...catch` lets you handle errors without stopping the script.
* Syntax:

  ```js
  try {
    // code that may throw
  } catch (err) {
    // error handling
  }
  ```

<br>

### 🔹 How it works

1. Code in `try` runs.
2. If no error → `catch` is skipped.
3. If error → `try` stops, `catch` runs with the error object.

<br>

### 🔹 Limitations

* Only works for **runtime errors** (valid JS, fails during execution).
* Doesn’t catch **syntax/parse-time errors**.
* Works **synchronously**:

  * Fails for delayed code (e.g., `setTimeout`) unless wrapped inside its own `try...catch`.

<br>

### 🔹 Error Object

* Passed automatically to `catch`.
* Common properties:

  * `name` → error type (e.g., `ReferenceError`)
  * `message` → description
  * `stack` → call trace (non-standard but common)

<br>

### 🔹 Optional Catch Binding

* `catch` can omit the error variable if not needed:

  ```js
  try { ... } catch { ... }
  ```

<br>

### 🔹 Throwing Errors

* Create and throw your own errors using `throw`.
* Can throw any value, but best to use error objects:

  ```js
  throw new Error("Something went wrong");
  throw new SyntaxError("Invalid format");
  ```

<br>

### 🔹 Rethrowing Technique

* A `catch` gets **all errors**, but should only handle the ones it knows.
* Unknown errors should be **re-thrown**.

  ```js
  try { ... } catch (err) {
    if (err instanceof SyntaxError) {
      // handle
    } else {
      throw err; // rethrow
    }
  }
  ```

<br>

### 🔹 `finally` Block

* Always runs:

  * After `try`, if no error.
  * After `catch`, if error happened.
* Useful for cleanup, finishing measurements, closing connections, etc.
* Runs even if there’s a `return` inside `try`.

<br>

### 🔹 `try...finally`

* Can be used without `catch` when you don’t want to handle errors but still want cleanup code to run.

<br>

### 🔹 Global Error Handling

* If an error isn’t caught, environments provide global handlers.
* In browsers:

  ```js
  window.onerror = function(message, url, line, col, error) {
    // log or report
  };
  ```
* Used mainly for logging/reporting, not recovery.

<br>

### 🔹 Summary

* `try...catch` handles runtime errors safely.
* `throw` lets you create custom errors.
* Always rethrow unknown errors for clarity.
* Use `finally` for guaranteed cleanup.
* Global handlers catch “falling out” errors.
