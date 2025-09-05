
## 🔹 Class Inheritance in JavaScript

1. **Basic idea**

   * `class Child extends Parent` → Child inherits Parent’s methods.
   * Internally: `Child.prototype.__proto__ = Parent.prototype`.

2. **Method lookup order**

   * Engine checks:

     1. Object itself
     2. Child prototype
     3. Parent prototype

3. **super keyword**

   * `super.method()` → calls parent method.
   * `super()` → calls parent constructor (must be first in derived constructors).

4. **Constructors in derived classes**

   * If no constructor is written → JS generates:

     ```js
     constructor(...args) {
       super(...args);
     }
     ```
   * If you define your own constructor → must call `super(...)` before using `this`.

5. **Arrow functions**

   * Arrow functions have no `super` or `this` of their own; they use the surrounding context.

6. **Overriding methods/fields**

   * Methods: overridden methods in child replace parent’s, but can call parent via `super`.
   * Fields: parent constructor uses its own field values, not child’s (different from methods).

7. **\[\[HomeObject]]**

   * Internal property that makes `super` work correctly.
   * Bound to where the method is defined.
   * Copying a method with `super` to another object may cause wrong behavior.

<br>

## 🔹 Tasks & Solutions

### 1. **Error creating an instance**

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Rabbit extends Animal {
  constructor(name) {
    super(name);           // ✅ must call super first
    this.created = Date.now();
  }
}

let rabbit = new Rabbit("White Rabbit");
alert(rabbit.name); // White Rabbit
```

<br>

### 2. **Extended Clock**

```js
// clock.js
class Clock {
  constructor({ template }) {
    this.template = template;
  }

  render() {
    let date = new Date();

    let hours = String(date.getHours()).padStart(2, '0');
    let mins = String(date.getMinutes()).padStart(2, '0');
    let secs = String(date.getSeconds()).padStart(2, '0');

    let output = this.template
      .replace('h', hours)
      .replace('m', mins)
      .replace('s', secs);

    console.log(output);
  }

  stop() {
    clearInterval(this.timer);
  }

  start() {
    this.render();
    this.timer = setInterval(() => this.render(), 1000);
  }
}
```

```js
// extended-clock.js
class ExtendedClock extends Clock {
  constructor(options) {
    super(options);
    let { precision = 1000 } = options;
    this.precision = precision;
  }

  start() {
    this.render();
    this.timer = setInterval(() => this.render(), this.precision);
  }
}
```

<br>

## 🔹 Quick Summary

* `extends` sets up prototype inheritance.
* Must call `super()` before using `this` in derived constructors.
* Methods can call parent ones via `super.method()`.
* Arrow functions inherit `this` and `super` from the outer scope.
* `[[HomeObject]]` is why `super` works correctly.
