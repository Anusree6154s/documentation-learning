
### Primitives vs Objects

* **Primitives (string, number, boolean, etc.)** → copied by **value**.
* **Objects** → copied by **reference** (variable stores memory address, not object itself).

<br>

### Copying Objects

* Copying a variable with an object copies its **reference**, not the actual object.
* Both variables point to the **same object** → changes via one are visible via the other.

<br>

### Comparison by Reference

* Two variables are **equal only if they reference the same object**.
* Different objects are not equal, even if identical in structure/content.

<br>

### `const` Objects

* Declaring `const user = {…}` prevents reassignment of `user`.
* But object **properties can still be changed**.

<br>

### Cloning & Merging

* **Manual copy with loop** → creates shallow independent object.
* **`Object.assign(dest, ...sources)`**

  * Copies properties into target object.
  * Can be used for shallow cloning: `let clone = Object.assign({}, user)`.
* **Spread syntax** → `let clone = {...user}` (shallow copy).

<br>

### Shallow vs Deep Cloning

* **Shallow copy** → nested objects are still shared (same reference).
* **Deep copy** → nested objects also cloned independently.

<br>

### `structuredClone`

* Built-in method for **deep cloning**.
* Supports most data types (objects, arrays, circular references).
* **Limitations** → cannot clone functions or special objects (like DOM nodes).

<br>

### Libraries

* For advanced deep cloning → use utilities like **Lodash’s `_.cloneDeep()`**.

<br>

⚡ **Summary:**

* Objects are stored/copied by reference.
* `Object.assign` / spread → shallow copy.
* `structuredClone` or libraries → deep copy (independent objects).

