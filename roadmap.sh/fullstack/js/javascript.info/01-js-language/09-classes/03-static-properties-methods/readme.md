
# 📌 Static Properties & Methods in JavaScript

## 🔹 Static Methods

* Declared with the `static` keyword.
* Belong to the **class itself**, not to instances.
* Called **on the class**, not on objects.
* Example:

  ```js
  class User {
    static greet() { return "Hello!"; }
  }
  User.greet(); // ✅ works
  new User().greet(); // ❌ Error
  ```

<br>

## 🔹 When to Use

* Utility methods that don’t depend on object data.
* Example: comparison function for sorting:

  ```js
  class Article {
    constructor(title, date) {
      this.title = title;
      this.date = date;
    }
    static compare(a, b) {
      return a.date - b.date;
    }
  }

  let articles = [
    new Article("HTML", new Date(2019,1,1)),
    new Article("CSS", new Date(2019,0,1)),
    new Article("JS", new Date(2019,11,1))
  ];
  articles.sort(Article.compare);
  ```

<br>

## 🔹 Factory Methods

* Alternative ways to create objects.
* Example:

  ```js
  class Article {
    constructor(title, date) {
      this.title = title;
      this.date = date;
    }
    static createTodays() {
      return new this("Today's digest", new Date());
    }
  }
  let article = Article.createTodays();
  ```

<br>

## 🔹 Static Properties

* Declared with `static` before property.
* Belong to the class itself.
* Example:

  ```js
  class Article {
    static publisher = "Ilya Kantor";
  }
  console.log(Article.publisher); // Ilya Kantor
  ```

<br>

## 🔹 Inheritance of Static Members

* `extends` also works for **static** properties & methods.

* Example:

  ```js
  class Animal {
    static planet = "Earth";
    static compare(a, b) {
      return a.speed - b.speed;
    }
  }
  class Rabbit extends Animal {}

  console.log(Rabbit.planet); // Earth (inherited)
  ```

* Internally:

  * `Rabbit.__proto__ === Animal` (for statics) ✅
  * `Rabbit.prototype.__proto__ === Animal.prototype` (for instance methods) ✅

<br>

## 🔹 Summary

* `static` → methods/properties belong to **class, not object**.
* Useful for:

  * Helpers (`Math.max`, `JSON.parse`, etc.).
  * Factory functions.
  * Class-level constants.
* Static members are **inherited** via `extends`.

<br>

# 📝 Task: `class Rabbit extends Object`

### Problem Code:

```js
class Rabbit extends Object {
  constructor(name) {
    this.name = name;
  }
}
let rabbit = new Rabbit("Rab");
alert(rabbit.hasOwnProperty("name")); // ❌ Error
```

### ❌ Why Error?

* When a class extends another, we must call `super()` in constructor **before using `this`**.
* `Object` has its own constructor, so `super()` is required.

<br>

### ✅ Fixed Code:

```js
class Rabbit extends Object {
  constructor(name) {
    super(); // ✅ call parent constructor
    this.name = name;
  }
}

let rabbit = new Rabbit("Rab");
alert(rabbit.hasOwnProperty("name")); // true
```
