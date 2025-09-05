
### **Primitives vs Objects**

* **Primitive** → single value of one of 7 types: `string`, `number`, `bigint`, `boolean`, `symbol`, `null`, `undefined`.
* **Object** → can store multiple values as properties (e.g., `{name: "John"}`), functions included.
* Objects are “heavier” (require more resources), primitives are lightweight.

<br>

### **Primitives with Methods**

* JS allows primitives to be used **like objects** (e.g., `"hello".toUpperCase()`).
* Mechanism:

  1. A temporary **wrapper object** (e.g., `String`, `Number`, `Boolean`, `Symbol`, `BigInt`) is created.
  2. The method is executed on it.
  3. The wrapper is destroyed → primitive remains intact.
* Example:

  ```js
  let str = "Hello";
  str.toUpperCase(); // "HELLO"
  ```
* Numbers also have methods, e.g., `toFixed(n)`:

  ```js
  let n = 1.23456;
  n.toFixed(2); // "1.23"
  ```

<br>

### **Wrapper Objects**

* Wrapper constructors (`new Number()`, `new String()`, `new Boolean()`) **exist but should not be used**.

  * They create objects, not primitives.
  * Example:

    ```js
    typeof 0;              // "number"
    typeof new Number(0);  // "object"
    if (new Number(0)) alert("zero is truthy!?"); // runs!
    ```
* ✅ Without `new` → converts values into primitives:

  ```js
  Number("123"); // 123
  Boolean("");   // false
  String(123);   // "123"
  ```

<br>

### **Special Cases**

* `null` and `undefined` have **no methods** and no wrapper objects.

  * Accessing properties throws an error:

    ```js
    null.test; // Error
    ```

<br>

### **Summary**

* Primitives (except `null` and `undefined`) provide methods via temporary wrapper objects.
* Wrapper constructors with `new` → ❌ not recommended.
* Type conversion functions (`Number()`, `String()`, `Boolean()`) → ✅ useful.
* Null/undefined → most primitive, no methods.
\