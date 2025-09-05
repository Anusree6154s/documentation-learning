
### Constructor & `new`

* `{...}` creates one object, but constructors + `new` allow many similar objects.
* **Constructor function rules:**

  * Name starts with a capital letter.
  * Should be called only with `new`.

<br>

### How `new` works

1. Creates an empty object → assigns it to `this`.
2. Executes function body (adds properties/methods to `this`).
3. Returns `this` (implicitly).

Example:

```js
function User(name) {
  this.name = name;
  this.isAdmin = false;
}
let user = new User("Jack");
```

<br>

### Alternative forms

* **Immediately called constructor**

  ```js
  let user = new function() {
    this.name = "John";
    this.isAdmin = false;
  };
  ```
* **`new.target`**

  * `undefined` if function called without `new`.
  * Equals the constructor if called with `new`.
  * Can auto-fix missing `new`.

<br>

### Return in constructors

* If returns **object** → that object is returned.
* If returns **primitive or nothing** → `this` is returned.

<br>

### Parentheses

* Parentheses after `new` can be omitted:

  ```js
  let user = new User;
  ```

<br>

### Methods in constructor

* Can add methods directly:

  ```js
  function User(name) {
    this.name = name;
    this.sayHi = () => alert("Hi, I’m " + this.name);
  }
  ```

<br>

### Summary

* Constructors = regular functions, named with capital letter, used with `new`.
* `new` automates object creation via `this`.
* Can build many similar objects quickly.
* Built-in constructors: `Date`, `Set`, etc.

<br>

### Tasks

**1. Two functions – one object**

* Possible if both return the same external object.

```js
let obj = {};
function A() { return obj; }
function B() { return obj; }
alert(new A() == new B()); // true
```

**2. Calculator constructor**

```js
function Calculator() {
  this.read = function() {
    this.a = +prompt("a?", 0);
    this.b = +prompt("b?", 0);
  };
  this.sum = () => this.a + this.b;
  this.mul = () => this.a * this.b;
}
```

**3. Accumulator constructor**

```js
function Accumulator(startingValue) {
  this.value = startingValue;
  this.read = function() {
    this.value += +prompt("Enter a number:", 0);
  };
}
```