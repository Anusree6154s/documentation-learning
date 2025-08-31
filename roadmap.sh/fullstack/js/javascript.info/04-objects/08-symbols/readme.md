
### **Symbols in JavaScript**

* **Definition**: A `Symbol` is a *primitive unique identifier*.
* **Creation**:

  ```js
  let id = Symbol("id"); // optional description for debugging
  ```

<br>

### **Key Properties**

* **Uniqueness**: Every `Symbol()` is unique, even with the same description.
* **Not auto-converted to string**:

  * `alert(Symbol("id")); // Error`
  * Use `.toString()` or `.description` to display.

<br>

### **Symbols as Object Keys**

* Only **strings** and **symbols** can be property keys.
* Safer than strings → avoids accidental overwrite/conflicts.
* Example:

  ```js
  let user = { name: "John" };
  let id = Symbol("id");
  user[id] = 123;
  ```

<br>

### **Behavior in Objects**

* Must use **square brackets** in object literals:

  ```js
  let user = { [id]: 123 };
  ```
* **Hidden from iteration**:

  * `for…in`, `Object.keys()` ignore symbols.
  * Accessible via `user[id]`.
  * `Object.assign` copies symbols too.
* Can still be retrieved via `Object.getOwnPropertySymbols()` or `Reflect.ownKeys()`.

<br>

### **Global Symbols**

* Use `Symbol.for(key)` to access/create global symbols (same across code parts).
* `Symbol.keyFor(sym)` → gets the key of a global symbol.
* Example:

  ```js
  let a = Symbol.for("id");
  let b = Symbol.for("id");
  a === b; // true
  ```

<br>

### **System (Well-known) Symbols**

* Predefined symbols that change language behavior:

  * `Symbol.iterator` – for making objects iterable.
  * `Symbol.toPrimitive` – customize object-to-primitive conversion.
  * `Symbol.hasInstance`, `Symbol.isConcatSpreadable`, etc.

<br>

### **Use Cases**

1. **Hidden object properties** – safe from overwriting & iteration.
2. **Global shared identifiers** – consistent across the app.
3. **System hooks** – tweak built-in JS behaviors.
