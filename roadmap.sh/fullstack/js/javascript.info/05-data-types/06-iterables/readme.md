

### 🔹 What Are Iterables

* **Iterable objects** = objects usable in `for..of`.
* **Arrays** and **strings** are built-in iterables.
* Any object can be made iterable by implementing `Symbol.iterator`.

<br>

### 🔹 Symbol.iterator

* An object is iterable if it has `obj[Symbol.iterator]()` method.
* `Symbol.iterator()` must return an **iterator object** with a `next()` method.
* `next()` must return:

  ```js
  { done: Boolean, value: any }
  ```

  * `done: false` → return value.
  * `done: true` → iteration finished.

<br>

### 🔹 Example: Range Iterable

```js
let range = {
  from: 1,
  to: 5,
  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },
  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    }
    return { done: true };
  }
};
for (let num of range) alert(num); // 1..5
```

* Here `range` is both the iterable and the iterator.
* Downside: can’t run two independent loops at once.

<br>

### 🔹 Key Ideas

* **Separation of concerns**: iterable object vs. iterator object.
* Iterators can also be **infinite** (e.g., random numbers, endless ranges).
* Use `break` to stop infinite loops.

<br>

### 🔹 Built-in Iterables

* **Arrays, Strings, Maps, Sets, TypedArrays, arguments, DOM collections**.
* String iteration is **Unicode-safe** (handles surrogate pairs correctly).

<br>

### 🔹 Manual Iterator Usage

```js
let str = "Hello";
let iterator = str[Symbol.iterator]();
console.log(iterator.next()); // {value: "H", done: false}
```

* Gives full control (pause/resume iteration).

<br>

### 🔹 Array-like vs Iterable

* **Iterable** → has `Symbol.iterator` (usable in `for..of`).
* **Array-like** → has numeric indexes + `length`, but no iterator.

  ```js
  let arrayLike = {0: "Hi", 1: "Bye", length: 2}; // array-like, not iterable
  ```
* Strings are both **array-like** and **iterable**.

<br>

### 🔹 Array.from

* Converts **iterable** or **array-like** into a real `Array`.
* Syntax:

  ```js
  Array.from(obj, [mapFn, thisArg])
  ```
* Examples:

  ```js
  Array.from(range); // [1,2,3,4,5]
  Array.from("𝒳😂"); // ["𝒳", "😂"]
  Array.from(range, x => x*x); // squares: [1,4,9,16,25]
  ```

<br>

### ✅ Summary

* Objects with `Symbol.iterator` are **iterable**.
* Iterators return `{done, value}` from `next()`.
* `for..of` uses `Symbol.iterator` automatically.
* **Array-like ≠ iterable** (but may overlap).
* `Array.from` converts iterable/array-like → real array (with optional mapping).
