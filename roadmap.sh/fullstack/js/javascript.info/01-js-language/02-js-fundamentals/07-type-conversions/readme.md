
## 🔹 Type Conversions in JavaScript

### 1. **String Conversion**

* Happens automatically when something needs to be shown as text (e.g., in `alert()`).
* Explicit conversion → `String(value)`.
* Examples:

  ```js
  let value = true;
  alert(typeof value); // boolean

  value = String(value);
  alert(typeof value); // string
  ```
* Results:

  * `true` → `"true"`
  * `false` → `"false"`
  * `null` → `"null"`
  * `undefined` → `"undefined"`

<br>

### 2. **Numeric Conversion**

* Happens automatically in math operations.
* Explicit conversion → `Number(value)`.
* Examples:

  ```js
  alert("6" / "2"); // 3 (strings converted to numbers)

  let str = "123";
  let num = Number(str);
  alert(typeof num); // number
  ```
* Conversion rules:

| Value         | Becomes |
| <br><br><br><br>- | <br><br>- |
| `undefined`   | `NaN`   |
| `null`        | `0`     |
| `true`        | `1`     |
| `false`       | `0`     |
| `"   123   "` | `123`   |
| `"123z"`      | `NaN`   |

<br>

### 3. **Boolean Conversion**

* Happens automatically in logical conditions.
* Explicit conversion → `Boolean(value)`.
* Examples:

  ```js
  alert(Boolean(1));    // true
  alert(Boolean(0));    // false
  alert(Boolean("hi")); // true
  alert(Boolean(""));   // false
  ```
* Conversion rules:

| Value                                 | Becomes |
| <br><br><br><br><br><br><br><br><br><br><br><br>- | <br><br>- |
| `0`, `""`, `null`, `undefined`, `NaN` | `false` |
| Any other value                       | `true`  |

⚠️ Special cases:

* `"0"` (string) → `true`
* `" "` (space string) → `true`

<br>

### 4. **Summary**

* **String conversion** → `String(value)` → obvious, e.g., `true → "true"`.
* **Number conversion** → `Number(value)` → follows strict rules (`null → 0`, `undefined → NaN`).
* **Boolean conversion** → `Boolean(value)` → “empty” values are `false`, all others `true`.
