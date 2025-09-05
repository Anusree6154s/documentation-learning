
## Prototype methods, objects without `__proto__`

### Modern ways to get/set prototypes

* `Object.getPrototypeOf(obj)` → returns the `[[Prototype]]` of `obj`.
* `Object.setPrototypeOf(obj, proto)` → sets the `[[Prototype]]` of `obj` to `proto`.
* `Object.create(proto[, descriptors])` → creates a new object with a given prototype and optional property descriptors.

✅ Example:

```js
let animal = { eats: true };
let rabbit = Object.create(animal, { jumps: { value: true } });
```

<br>

### Object cloning with descriptors

```js
let clone = Object.create(
  Object.getPrototypeOf(obj), 
  Object.getOwnPropertyDescriptors(obj)
);
```

This copies everything:

* enumerable & non-enumerable properties
* data & accessor properties
* correct prototype

<br>

### Brief history of prototype management

1. **Oldest** → Constructor function `prototype` property.
2. **2012** → `Object.create` added.
3. **Browsers** → Implemented `obj.__proto__` (non-standard).
4. **2015** → Standardized `Object.getPrototypeOf` / `Object.setPrototypeOf`.

   * `__proto__` moved to Annex B (browser-only).
5. **2022** → `__proto__` allowed only inside object literals `{ __proto__: ... }`.

   * But **not** as `obj.__proto__` getter/setter.

<br>

### Why `__proto__` is discouraged

* Changing prototypes at runtime (`Object.setPrototypeOf` or `obj.__proto__ = ...`) → **very slow**, breaks engine optimizations.
* `__proto__` as a property is tricky:

  ```js
  let obj = {};
  obj["__proto__"] = "value"; // ignored → doesn't work as expected
  ```

<br>

### Prototype-less (“very plain”) objects

* Use `Object.create(null)` or `{ __proto__: null }`.
* These objects:

  * Have no inherited properties/methods.
  * `__proto__` is treated as a normal key.
  * Perfect for dictionaries with user-generated keys.

⚠ Downside: No `toString` or other methods from `Object.prototype`.

✅ Example:

```js
let dict = Object.create(null);
dict["__proto__"] = "test"; // works fine
```

<br>

### Summary

* **Create objects**

  * `{ __proto__: ... }` → concise
  * `Object.create(proto, descriptors)` → powerful (supports descriptors)
* **Clone objects** with `Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj))`.
* **Modern prototype methods** → `Object.getPrototypeOf`, `Object.setPrototypeOf`.
* **Avoid `__proto__`** getter/setter except in object literals.
* **Use null-prototype objects** for safe dictionaries.

<br>

## Tasks

### 1. Add `toString` to dictionary

```js
let dictionary = Object.create(null);

Object.defineProperty(dictionary, "toString", {
  value() {
    return Object.keys(this).join(",");
  },
  enumerable: false // so it won’t appear in for..in
});

// test
dictionary.apple = "Apple";
dictionary.__proto__ = "test";

for (let key in dictionary) alert(key); 
// → apple, __proto__

alert(dictionary); // → "apple,__proto__"
```

<br>

### 2. The difference between calls

```js
function Rabbit(name) {
  this.name = name;
}
Rabbit.prototype.sayHi = function() {
  alert(this.name);
};

let rabbit = new Rabbit("Rabbit");
```

* `rabbit.sayHi();` → `"Rabbit"` (method called with `this = rabbit`).
* `Rabbit.prototype.sayHi();` → `undefined` (no `name` in prototype).
* `Object.getPrototypeOf(rabbit).sayHi();` → same as above → `undefined`.
* `rabbit.__proto__.sayHi();` → same as above → `undefined`.

✅ Only the **first call** prints `"Rabbit"`.
