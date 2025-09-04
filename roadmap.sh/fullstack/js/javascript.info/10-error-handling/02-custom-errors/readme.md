
### 1. Custom Errors in JavaScript

* JavaScript allows `throw` with *any* value, but best practice is to inherit from **Error**.
* Inheriting from `Error` makes `instanceof` checks possible (`err instanceof Error`).

<br>

### 2. Error Hierarchy

* As apps grow, we create specialized error classes.

  * Example:

    * `ValidationError` (general validation issues).
    * `PropertyRequiredError` (missing specific property).
    * `HttpError → HttpTimeoutError` for network cases.

<br>

### 3. Extending `Error`

```js
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}
```

* Always call `super(message)` in constructors.
* Reset `this.name` to match your custom class name.
* `err.stack` is automatically available (non-standard, but supported everywhere).

<br>

### 4. Validation Example

```js
function readUser(json) {
  let user = JSON.parse(json);

  if (!user.age) throw new ValidationError("No field: age");
  if (!user.name) throw new ValidationError("No field: name");

  return user;
}
```

Handling:

```js
try {
  readUser('{ "age": 25 }');
} catch (err) {
  if (err instanceof ValidationError) { ... }
  else if (err instanceof SyntaxError) { ... }
  else throw err; // rethrow unknown
}
```

✅ Always **rethrow unknown errors**.

<br>

### 5. Subclassing Errors

```js
class PropertyRequiredError extends ValidationError {
  constructor(property) {
    super("No property: " + property);
    this.name = "PropertyRequiredError";
    this.property = property;
  }
}
```

<br>

### 6. Avoid Repeating `this.name`

```js
class MyError extends Error {
  constructor(message) {
    super(message);
    this.name = this.constructor.name; // auto-assigns class name
  }
}
```

* All custom errors extend `MyError` → cleaner code.

<br>

### 7. Wrapping Exceptions

* Create higher-level errors to abstract low-level ones.
* Example: `ReadError` wraps `SyntaxError` or `ValidationError`.

```js
class ReadError extends Error {
  constructor(message, cause) {
    super(message);
    this.name = "ReadError";
    this.cause = cause; // keep original error
  }
}
```

Usage:

```js
try {
  readUser('{bad json}');
} catch (e) {
  if (e instanceof ReadError) {
    console.log("Original error:", e.cause);
  } else {
    throw e;
  }
}
```

<br>

### 8. Summary

* ✅ Always `super(message)` when extending `Error`.
* ✅ Use `instanceof` for type checks (future-proof with inheritance).
* ✅ Rethrow unknown errors.
* ✅ Use a **base error class** (`MyError`) to auto-assign names.
* ✅ Use **wrapping exceptions** for higher-level error abstraction.
