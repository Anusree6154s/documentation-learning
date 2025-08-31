

## 🔹 Variables in JavaScript
- **Variable = named storage for data**.  
  Example:  
  ```js
  let message = "Hello!";
  alert(message); // Hello!
  ```

<br>

## 🔹 Declaring Variables
- **Use `let`** → modern way to declare variables.
- **Use `var`** → old style (avoid in modern code).
- **Use `const`** → declare constants (cannot be reassigned).

Examples:
```js
let user = "John";  // variable
const pi = 3.14159; // constant
var oldWay = "Still works, but avoid";
```

<br>

## 🔹 Assigning Values
- Variables can be declared first, then assigned:
  ```js
  let message;
  message = "Hello!";
  ```
- Or both in one line:
  ```js
  let message = "Hello!";
  ```

<br>

## 🔹 Changing Values
- You can **reassign values** with `let` and `var`:
  ```js
  let message = "Hello!";
  message = "World!";  // changed
  ```
- With `const`, reassignment is **not allowed**:
  ```js
  const myBirthday = "18.04.1982";
  myBirthday = "2000.01.01"; // ❌ Error
  ```

<br>

## 🔹 Copying Values
```js
let hello = "Hello world!";
let message = hello;

alert(hello);   // Hello world!
alert(message); // Hello world!
```

<br>

## 🔹 Naming Variables
- Must contain **letters, digits, `$`, `_`**
- Must **not start with a digit**
- Case-sensitive (`apple` ≠ `APPLE`)
- Common style → **camelCase**

✅ Valid:
```js
let userName;
let test123;
let $ = 1;
let _ = 2;
```

<amrk>❌ Invalid:</mark>
```js
let 1apple;    // starts with digit
let my-name;   // hyphen not allowed
```

<br>

## 🔹 Reserved Words
- Cannot use words like `let`, `class`, `return`, `function` as variable names.

<br>

## 🔹 Constants Naming
- **Runtime constants** → use normal naming:
  ```js
  const pageLoadTime = 1234; // value set at runtime
  ```
- **Hard-coded constants** → use UPPERCASE:
  ```js
  const COLOR_RED = "#F00";
  const COLOR_BLUE = "#00F";
  ```

<br>

## 🔹 Best Practices
- Use **meaningful names** (`userName`, `shoppingCart`).
- Avoid vague names like `data` or `value`.
- Don’t reuse variables unnecessarily → declare new ones instead.
