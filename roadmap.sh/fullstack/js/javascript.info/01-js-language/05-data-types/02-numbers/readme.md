
## 📌 Numbers in JavaScript

### Types

* **Regular numbers**: stored in 64-bit IEEE-754 (double precision floating point).
* **BigInt**: for integers beyond `-(2^53 - 1)` to `(2^53 - 1)`.

<br>

### Writing Numbers

* Underscores `_` can make numbers more readable:
  `1_000_000_000` → `1000000000`.
* Scientific notation with `e`:
  `1e9` = `1,000,000,000`, `1e-6` = `0.000001`.

<br>

### Numeral Systems

* **Hex**: `0xff` = 255
* **Binary**: `0b11111111` = 255
* **Octal**: `0o377` = 255
* `num.toString(base)` → converts number to string in base 2–36.

<br>

### Rounding

* `Math.floor(x)` → round down.
* `Math.ceil(x)` → round up.
* `Math.round(x)` → round to nearest.
* `Math.trunc(x)` → remove decimals.
* `toFixed(n)` → round to `n` decimals (returns string).

<br>

### Precision Issues

* Floating-point math has **rounding errors**.

  * `0.1 + 0.2 === 0.3` → `false`.
  * `0.1 + 0.2 = 0.30000000000000004`.
* Fix: use `toFixed()`, integer math (`*100` then `/100`), or rounding.
* Max safe integer: `Number.MAX_SAFE_INTEGER = 2^53 - 1`.

<br>

### Special Numbers

* `Infinity`, `-Infinity`, `NaN`.
* `isNaN(value)` → true if value converts to NaN.
* `Number.isNaN(value)` → true only if value is NaN (no type coercion).
* `isFinite(value)` → true if finite number (after conversion).
* `Number.isFinite(value)` → true if finite number, **without conversion**.
* `Object.is(a, b)` → strict comparison, handles `NaN` and `0 / -0`.

<br>

### Parsing Numbers

* `parseInt(str, base)` → extracts integer, supports bases.

  * `parseInt("100px")` → `100`.
  * `parseInt("ff", 16)` → `255`.
* `parseFloat(str)` → extracts float.

  * `parseFloat("12.5em")` → `12.5`.

<br>

### Math Object

* `Math.random()` → 0 ≤ x < 1.
* `Math.max(...nums)`, `Math.min(...nums)`.
* `Math.pow(n, power)` → exponentiation.
* Many more (trigonometry, constants, etc.).

<br>

## 📌 Tasks (Practice)

1. **Sum numbers from visitor**
   Prompt for two numbers → show sum. Watch out for string input (convert with `+`).

2. **Why `6.35.toFixed(1) == 6.3`?**

   * Floating-point precision issue.
   * Fix: use `Math.round(num * 10) / 10`.

3. **readNumber()**

   * Keep prompting until input is a valid number.
   * Empty input / cancel → return `null`.

4. **Infinite loop (i += 0.2)**

   * Due to floating-point precision, `i` never equals exactly `10`.

5. **random(min, max)**

   * Returns random float between `min` and `max`.

6. **randomInteger(min, max)**

   * Returns random integer, inclusive of both ends.
   * Use `Math.floor(random(min, max+1))`.

