

# 📌 Arrow Functions (Revisited)

### 🔹 Key Features

* **No own `this`** → takes `this` from the outer scope (lexical scoping).
* **No own `arguments`** → must use rest `...args` if needed.
* **Can’t be used with `new`** → not constructors.
* **No `super`** (used in classes – covered later).

<br>

### 🔹 Why they’re useful

* Great for **callbacks** (e.g., `forEach`, `setTimeout`, event handlers).
* Avoids losing `this` inside nested functions.
* Cleaner syntax for short functions.

<br>

### 🔹 Example: Preserving `this`

✅ Using arrow function (works as expected):

```js
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],

  showList() {
    this.students.forEach(
      student => console.log(this.title + ': ' + student)
    );
  }
};

group.showList();
```

❌ Using regular function (error):

```js
this.students.forEach(function(student) {
  console.log(this.title + ': ' + student); // Error
});
```

<br>

### 🔹 Arrow vs `.bind(this)`

* `.bind(this)` → creates a permanently bound function.
* Arrow function → doesn’t bind, just inherits `this` from outer scope.

<br>

### 🔹 Example: `arguments` with arrows

✅ Arrow avoids extra variables:

```js
function defer(f, ms) {
  return function() {
    setTimeout(() => f.apply(this, arguments), ms);
  };
}
```

❌ Regular function needs manual handling:

```js
function defer(f, ms) {
  return function(...args) {
    let ctx = this;
    setTimeout(function() {
      return f.apply(ctx, args);
    }, ms);
  };
}
```

<br>

### 🔹 Summary

* **Arrow functions cannot**:

  * Have their own `this`
  * Have their own `arguments`
  * Be used with `new`
  * Have `super`

* **Best use case**: short callbacks where you want to keep the surrounding context.
