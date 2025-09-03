

## 🔹 `instanceof` Basics

* Syntax:

  ```js
  obj instanceof Class
  ```
* Returns `true` if `obj` belongs to `Class` or any class inheriting from it.
* Works with:

  * ES6 classes
  * Constructor functions
  * Built-in classes (`Array`, `Date`, etc.)

<br>

## 🔹 How it Works (Algorithm)

1. If `Class` has a static method `Symbol.hasInstance` → call it:
   `Class[Symbol.hasInstance](obj)`

   * Must return `true/false`.
   * Allows **custom logic**.
2. Else → check prototype chain:

   ```js
   obj.__proto__ === Class.prototype ?
   obj.__proto__.__proto__ === Class.prototype ?
   ...
   ```

   * If found → `true`
   * If end of chain reached → `false`.

<br>

## 🔹 Example: Custom `Symbol.hasInstance`

```js
class Animal {
  static [Symbol.hasInstance](obj) {
    return !!obj.canEat;
  }
}
let obj = { canEat: true };
alert(obj instanceof Animal); // true
```

<br>

## 🔹 Key Notes

* `instanceof` checks **prototypes**, not the constructor function itself.
* Equivalent check:

  ```js
  Class.prototype.isPrototypeOf(obj)
  ```
* Changing `Class.prototype` breaks old instances:

  ```js
  function Rabbit() {}
  let rabbit = new Rabbit();
  Rabbit.prototype = {};
  alert(rabbit instanceof Rabbit); // false
  ```

<br>

## 🔹 Alternatives

### 1. `Object.prototype.toString.call(value)`

* Returns a string `[object Type]`.
* Works with primitives + built-ins.
* Example:

  ```js
  let s = Object.prototype.toString;
  s.call(123); // [object Number]
  s.call([]);  // [object Array]
  s.call(null); // [object Null]
  ```

### 2. `Symbol.toStringTag`

* Allows customization:

  ```js
  let user = { [Symbol.toStringTag]: "User" };
  {}.toString.call(user); // [object User]
  ```

<br>

## 🔹 Comparison Table

| Method                    | Works For                       | Returns        |
| <br><br><br><br><br><br><br><br>- | <br><br><br><br><br><br><br><br><br><br>- | <br><br><br><br>-- |
| `typeof`                  | Primitives only                 | string         |
| `{}.toString.call(value)` | Primitives + built-ins + custom | `[object ...]` |
| `instanceof`              | Objects (class hierarchy)       | true/false     |

<br>

## 🔹 Task: Strange `instanceof`

```js
function A() {}
function B() {}

A.prototype = B.prototype = {};

let a = new A();
alert(a instanceof B); // true
```

✅ **Why?**

* `instanceof` only checks if `B.prototype` is in `a`’s prototype chain.
* Since `A.prototype = B.prototype = {}`, both share the same object.
* So `a.__proto__ === B.prototype` → `true`.
