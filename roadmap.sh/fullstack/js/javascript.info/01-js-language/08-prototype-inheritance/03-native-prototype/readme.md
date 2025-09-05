

# 📌 Native Prototypes in JavaScript

## 🔹 Basics

* Every built-in constructor function (Object, Array, Function, etc.) has a **prototype**.
* Objects created with `{}` or `new Object()` → inherit from **Object.prototype**.
* Example:

  ```js
  let obj = {};
  obj.__proto__ === Object.prototype; // true
  ```

<br>

## 🔹 Prototype Chain

* Built-in objects (Array, Date, Function, …) also inherit from prototypes:

  * `Array.prototype`
  * `Function.prototype`
  * etc.
* All eventually link to **Object.prototype → null**.
* Example:

  ```js
  let arr = [1,2,3];
  arr.__proto__ === Array.prototype; // true
  arr.__proto__.__proto__ === Object.prototype; // true
  arr.__proto__.__proto__.__proto__ === null; // top
  ```

<br>

## 🔹 Method Resolution

* Closest prototype method is used.
* Example:

  ```js
  [1,2,3].toString(); // "1,2,3" (from Array.prototype)
  {}.toString();      // "[object Object]" (from Object.prototype)
  ```

<br>

## 🔹 Functions

* Functions are objects created by `Function` constructor.
* They inherit from **Function.prototype**, then **Object.prototype**.
* Example:

  ```js
  function f() {}
  f.__proto__ === Function.prototype; // true
  ```

<br>

## 🔹 Primitives

* Strings, Numbers, Booleans → not objects, but get **temporary wrapper objects**.
* Methods come from:

  * `String.prototype`
  * `Number.prototype`
  * `Boolean.prototype`
* Example:

  ```js
  "hi".toUpperCase(); // HI
  ```
* `null` and `undefined` ❌ have no wrappers.

<br>

## 🔹 Modifying Native Prototypes

* Can add new methods:

  ```js
  String.prototype.show = function() { alert(this); };
  "Hello".show(); // Hello
  ```
* ❌ Not recommended → conflicts with other code.
* ✅ Allowed for **polyfills** (implementing missing standard methods).

Example Polyfill:

```js
if (!String.prototype.repeat) {
  String.prototype.repeat = function(n) {
    return new Array(n+1).join(this);
  };
}
"Hi".repeat(3); // HiHiHi
```

<br>

## 🔹 Borrowing Methods

* Methods can be borrowed from prototypes.
* Example: Using `Array.prototype.join` on array-like objects:

  ```js
  let obj = {0: "Hello", 1: "World", length: 2};
  obj.join = Array.prototype.join;
  obj.join(", "); // "Hello, World"
  ```

<br>

## 📌 Summary

* All built-ins store **methods in their prototypes**.
* Objects store only **data**.
* Prototypes chain up to `Object.prototype → null`.
* Primitives use wrapper objects for methods.
* Avoid modifying native prototypes (except polyfills).
* Method borrowing lets non-arrays use Array methods, etc.

<br>

# 📝 Tasks

### 1. Add `f.defer(ms)` to all functions

```js
Function.prototype.defer = function(ms) {
  setTimeout(this, ms);
};

function f() { alert("Hello!"); }
f.defer(1000); // Hello after 1s
```

<br>

### 2. Add `f.defer(ms)(...args)`

```js
Function.prototype.defer = function(ms) {
  let f = this;
  return function(...args) {
    setTimeout(() => f.apply(this, args), ms);
  };
};

function f(a, b) { alert(a + b); }
f.defer(1000)(1, 2); // 3 after 1s
```
