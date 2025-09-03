

## 🔹 Basic Class Syntax
```js
class MyClass {
  constructor(name) {
    this.name = name;   // property
  }
  sayHi() {            // method
    alert(this.name);
  }
}
let user = new MyClass("John");
user.sayHi(); // John
```
- `class` defines a template.
- `constructor` runs automatically on `new`.
- Methods are added to `prototype`.

<br>

## 🔹 What is a Class?
- Technically, a **class is a function**.
```js
class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}
alert(typeof User); // function
```
- Class methods live on `User.prototype`.

<br>

## 🔹 Class vs Function + Prototype
Equivalent definition without `class`:
```js
function User(name) {
  this.name = name;
}
User.prototype.sayHi = function() {
  alert(this.name);
};
let user = new User("John");
user.sayHi();
```
So, **class = constructor function + prototype methods**, but with extra rules:
- Must call with `new`.
- Always strict mode.
- Methods are non-enumerable.

<br>

## 🔹 Class Expressions
- Classes can be stored in variables, returned, or anonymous.
```js
let User = class {
  sayHi() { alert("Hello"); }
};
```

Named class expression (name only visible inside):
```js
let User = class MyClass {
  sayHi() { alert(MyClass); }
};
new User().sayHi(); // works
// MyClass not accessible outside
```

<br>

## 🔹 Dynamic Class Creation
```js
function makeClass(phrase) {
  return class {
    sayHi() { alert(phrase); }
  };
}
let User = makeClass("Hello!");
new User().sayHi(); // Hello!
```

<br>

## 🔹 Getters / Setters
```js
class User {
  constructor(name) { this.name = name; }
  get name() { return this._name; }
  set name(value) {
    if (value.length < 4) { alert("Too short!"); return; }
    this._name = value;
  }
}
let user = new User("John");
alert(user.name);   // John
user.name = "Al";   // Too short!
```

<br>

## 🔹 Computed Method Names
```js
class User {
  ["say" + "Hi"]() { alert("Hello!"); }
}
new User().sayHi(); // Hello!
```

<br>

## 🔹 Class Fields
- Properties defined directly in the class.
```js
class User {
  name = "John";  
  sayHi() { alert(`Hello, ${this.name}`); }
}
new User().sayHi(); // Hello, John
```
- Unlike prototype methods, **fields are per-object**.

<br>

## 🔹 Bound Methods with Class Fields
Problem: losing `this`
```js
class Button {
  constructor(value) { this.value = value; }
  click() { alert(this.value); }
}
let btn = new Button("Hello");
setTimeout(btn.click, 1000); // undefined
```

Solution: use arrow function in class field → auto binds `this`.
```js
class Button {
  constructor(value) { this.value = value; }
  click = () => { alert(this.value); }
}
let btn = new Button("Hello");
setTimeout(btn.click, 1000); // Hello
```

<br>

## 🔹 Summary: Class Syntax
```js
class MyClass {
  prop = "value";          // field
  constructor(arg) { ... } // constructor
  method() { ... }         // method
  get something() { ... }  // getter
  set something(v) { ... } // setter
  [Symbol.iterator]() { }  // computed/symbol method
}
```
- Class = special kind of function.
- Methods go on `prototype`.
- Always strict mode.
- Not just syntactic sugar — has unique behaviors.
