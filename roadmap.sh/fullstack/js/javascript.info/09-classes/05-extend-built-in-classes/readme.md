

### ✅ Extending Built-ins

* Built-in classes (`Array`, `Map`, `Set`, etc.) can be extended with `class ... extends ...`.
* Example:

```js
class PowerArray extends Array {
  isEmpty() {
    return this.length === 0;
  }
}

let arr = new PowerArray(1, 2, 5, 10, 50);
arr.isEmpty(); // false
```

<br>

### ✅ Built-in Methods Respect Subclass

* Methods like `.filter()`, `.map()`, `.slice()` return instances of the **extended class**, not just plain arrays.
* Because they use the object’s `constructor` property internally.
* Example:

```js
let filteredArr = arr.filter(item => item >= 10);
// filteredArr is PowerArray, so it also has isEmpty()
```

<br>

### ✅ Controlling Return Type → `Symbol.species`

* By default, subclassed built-ins return instances of the subclass.
* Can override behavior with a static getter `[Symbol.species]`.
* Example:

```js
class PowerArray extends Array {
  static get [Symbol.species]() { return Array; }
}
let arr = new PowerArray(1, 2, 5, 10, 50);
let filteredArr = arr.filter(item => item >= 10);
// filteredArr is now a plain Array, not PowerArray
```

<br>

### ✅ Other Collections

* `Map`, `Set`, and similar also use `Symbol.species`.
* Same rules apply as with `Array`.

<br>

### ✅ Static Inheritance Limitation

* Normally, static and instance methods are both inherited with `extends`.
* **Built-in classes are special**:

  * Their instances inherit properly (`Array.prototype` from `Object.prototype`).
  * But **static methods are not inherited**.
* Example:

  * `Array` has `Array.isArray()`.
  * `Object` has `Object.keys()`.
  * But `Array.keys()` (static) does not exist.
* Reason: Built-ins don’t share static inheritance chains like normal classes.

<br>

⚡ In short:

* You can extend built-ins to add custom behavior.
* Subclass instances are preserved in built-in methods unless overridden with `Symbol.species`.
* Built-in **static methods are not inherited**, only instance methods are.
