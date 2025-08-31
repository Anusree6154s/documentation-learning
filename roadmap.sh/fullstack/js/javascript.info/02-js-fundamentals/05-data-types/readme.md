
## 📌 JavaScript Data Types – Key Points

### 1. **Dynamic Typing**

* JavaScript is **dynamically typed** → variables can hold values of any type.
* Example:

  ```js
  let message = "hello";
  message = 123; // allowed
  ```

<br>

### 2. **Eight Basic Data Types**

#### 🔹 Primitive Types (7):

1. **Number**

   * For integers & floating-point numbers.
   * Special values: `Infinity`, `-Infinity`, `NaN`.

   ```js
   alert(1/0); // Infinity
   alert("not a number" / 2); // NaN
   ```

2. **BigInt**

   * For very large integers (beyond ±(2^53 - 1)).

   ```js
   const big = 123456789012345678901234567890n;
   ```

3. **String**

   * Must be inside quotes: `"`, `'`, or backticks `` ` ``.
   * Backticks support **template literals** with `${...}`.

   ```js
   let name = "John";
   alert(`Hello, ${name}`); // Hello, John
   ```

4. **Boolean**

   * Logical values: `true` / `false`.

   ```js
   let isGreater = 5 > 2; // true
   ```

5. **null**

   * Represents “nothing”, “empty”, or “unknown”.

   ```js
   let age = null;
   ```

6. **undefined**

   * Means “not assigned”.

   ```js
   let x;
   alert(x); // undefined
   ```

7. **Symbol**

   * Unique identifiers, mainly for objects.

#### 🔹 Non-Primitive Type (1):

8. **Object**

   * For collections and complex entities.
   * Functions are objects too.

<br>

### 3. **typeof Operator**

* Returns the type of a value as a string:

  ```js
  typeof 123;      // "number"
  typeof "hi";     // "string"
  typeof true;     // "boolean"
  typeof undefined;// "undefined"
  typeof null;     // "object" (bug in JS)
  typeof alert;    // "function"
  ```

<br>

### 4. **Summary**

* **7 primitives**: number, bigint, string, boolean, null, undefined, symbol.
* **1 non-primitive**: object.
* JavaScript allows flexible typing (variables can switch types).

<br>


## Diff between primitive and non primitive types

### 🔹 Primitive Data Types

* **Definition**: Basic, single-value types.
* **Examples**: `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, `bigint`.
* **Stored**: Directly in **stack memory** (value is stored directly).
* **Immutable**: Cannot be changed (e.g., strings).
* **Compared by value**.

<br>

### 🔹 Non-Primitive Data Types

* **Definition**: Complex data structures (collections, objects).
* **Examples**: `object`, `array`, `function`.
* **Stored**: In **heap memory** (variable stores a reference to the object).
* **Mutable**: Can be changed after creation.
* **Compared by reference**.

<br>

### ✅ **In one line**:
- **Primitive → single, immutable values (by value).**
- **Non-Primitive → collections/objects, mutable (by reference).**
