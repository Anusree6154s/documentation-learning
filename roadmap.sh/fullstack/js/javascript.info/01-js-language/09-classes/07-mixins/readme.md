

## 🔹 What are Mixins?

* In JavaScript, **a class can extend only one other class** (single inheritance).
* Sometimes we need to add extra functionality (like event handling, logging, etc.) to multiple classes.
* **Mixin** = a set of methods that can be added to a class **without using inheritance**.

👉 Think of them as "behavior packs" that can be copied into other classes.

<br>

## 🔹 Simple Mixin Example

```js
// mixin with reusable methods
let sayHiMixin = {
  sayHi() { alert(`Hello ${this.name}`); },
  sayBye() { alert(`Bye ${this.name}`); }
};

class User {
  constructor(name) {
    this.name = name;
  }
}

// copy methods into User.prototype
Object.assign(User.prototype, sayHiMixin);

new User("Dude").sayHi(); // Hello Dude!
```

✅ No inheritance → just **method copying**.

<br>

## 🔹 Mixins + Inheritance

Mixins themselves can use inheritance:

```js
let sayMixin = {
  say(phrase) { alert(phrase); }
};

let sayHiMixin = {
  __proto__: sayMixin,   // parent mixin
  sayHi() { super.say(`Hello ${this.name}`); },
  sayBye() { super.say(`Bye ${this.name}`); }
};

class User {
  constructor(name) { this.name = name; }
}
Object.assign(User.prototype, sayHiMixin);

new User("John").sayHi(); // Hello John
```

* `super.say()` works because the `[[HomeObject]]` of the method is the mixin itself.

<br>

## 🔹 Event Mixin (Real-world Example)

We can create a **reusable event system** for any class:

```js
let eventMixin = {
  on(eventName, handler) {
    if (!this._eventHandlers) this._eventHandlers = {};
    (this._eventHandlers[eventName] ||= []).push(handler);
  },

  off(eventName, handler) {
    let handlers = this._eventHandlers?.[eventName];
    if (!handlers) return;
    this._eventHandlers[eventName] =
      handlers.filter(h => h !== handler);
  },

  trigger(eventName, ...args) {
    this._eventHandlers?.[eventName]?.forEach(
      handler => handler.apply(this, args)
    );
  }
};
```

### Usage:

```js
class Menu {
  choose(value) {
    this.trigger("select", value);
  }
}

// add mixin to Menu
Object.assign(Menu.prototype, eventMixin);

let menu = new Menu();

// listen for "select"
menu.on("select", value => alert(`Value selected: ${value}`));

// trigger event
menu.choose("123"); // alerts: Value selected: 123
```

<br>

## 🔹 Summary

* **Mixin** = object with methods that can be added to a class.
* Implemented in JS by **copying methods** into a class prototype.
* Can provide **extra behaviors** (logging, events, animations, etc.).
* ⚠️ Risk: method name conflicts if two mixins define the same method.
