

### 🔹 Introduction

* **BigInt** → special numeric type in JavaScript for integers of arbitrary length.
* Created by:

  * Adding `n` to an integer literal → `123n`
  * Calling `BigInt()` constructor → `BigInt("123")`, `BigInt(10)`

<br>

### 🔹 Examples

```js
const bigint1 = 1234567890123456789012345678901234567890n;
const bigint2 = BigInt("1234567890123456789012345678901234567890");
const bigintFromNum = BigInt(10); // same as 10n
```

<br>

### 🔹 Math Operations

* Works with most math operators (`+`, `-`, `*`, `/`, `%`).
* Division returns **rounded bigint** (no decimals).

  ```js
  5n / 2n; // 2
  ```
* ❌ Cannot mix `BigInt` and `Number` directly.

  ```js
  1n + 2; // Error
  ```
* ✅ Convert explicitly using `BigInt()` or `Number()`.

  ```js
  BigInt(2) + 1n; // 3n
  Number(1n) + 2; // 3
  ```

<br>

### 🔹 Conversions

* Silent (no errors), but risk of **overflow/truncation** when converting large BigInt → Number.
* Unary `+` not allowed on BigInt:

  ```js
  +1n; // Error
  Number(1n); // OK
  ```

<br>

### 🔹 Comparisons

* Works across `BigInt` and `Number`.

  ```js
  2n > 1; // true
  ```
* Loose equality (`==`) works, strict equality (`===`) does not.

  ```js
  1 == 1n;   // true
  1 === 1n;  // false
  ```

<br>

### 🔹 Boolean Behavior

* In conditions:

  * `0n` → falsy
  * Any other BigInt → truthy
* Logical operators behave like with numbers:

  ```js
  1n || 2; // 1n
  0n || 2; // 2
  ```

<br>

### 🔹 Polyfills

* Hard to polyfill because BigInt changes operator behavior.
* **JSBI library** → provides bigint-like operations as functions.

  * Example:

    ```js
    a = JSBI.BigInt(789);
    c = JSBI.add(a, b);
    ```
* Babel plugin can convert JSBI → native BigInt for supported browsers.

<br>

✅ **Summary**:

* Use `BigInt` for very large integers beyond Number’s safe range.
* Can’t mix with normal numbers without explicit conversion.
* Works with most math/comparison operators.
* No reliable polyfill → use **JSBI** if cross-browser support needed.
