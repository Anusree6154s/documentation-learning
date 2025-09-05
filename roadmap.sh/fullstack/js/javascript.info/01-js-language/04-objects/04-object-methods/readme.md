
## 🔹 Object Methods & `this`

### Methods

* A **method** = function stored as an object property.

  ```js
  let user = {
    sayHi: function() { alert("Hello"); }
  };
  ```
* **Shorthand syntax** preferred:

  ```js
  let user = {
    sayHi() { alert("Hello"); }
  };
  ```

### `this` keyword

* `this` = the object **before the dot**.

  ```js
  let user = {
    name: "John",
    sayHi() { alert(this.name); }
  };
  user.sayHi(); // John
  ```

* Using `this` is safer than directly naming the object (e.g., `user.name`), since the object reference can change.

### Important rules

* `this` is **not bound** → its value depends on **how** the function is called, not where it’s written.
* Copying the same function to different objects → `this` changes:

  ```js
  function sayHi() { alert(this.name); }

  let user = { name: "John", f: sayHi };
  let admin = { name: "Admin", f: sayHi };

  user.f();   // John
  admin.f();  // Admin
  ```
* Call without object → `this == undefined` (in strict mode).

### Arrow functions & `this`

* Arrow functions don’t have their own `this`.
* They take `this` from the **outer (lexical) scope**.

  ```js
  let user = {
    firstName: "Ilya",
    sayHi() {
      let arrow = () => alert(this.firstName);
      arrow(); // Ilya
    }
  };
  ```

<br>

## 🔹 Tasks & Solutions

### 1. Using `"this"` in object literal

```js
function makeUser() {
  return {
    name: "John",
    ref: this
  };
}

let user = makeUser();
alert(user.ref.name);
```

* ❌ `undefined`, because inside `makeUser`, `this` refers to **nothing** (undefined in strict mode), not to the object being created.
* ✅ Correct way:

  ```js
  function makeUser() {
    return {
      name: "John",
      ref() {
        return this;
      }
    };
  }

  let user = makeUser();
  alert(user.ref().name); // John
  ```

<br>

### 2. Calculator Object

```js
let calculator = {
  read() {
    this.a = +prompt("Enter a:", 0);
    this.b = +prompt("Enter b:", 0);
  },
  sum() {
    return this.a + this.b;
  },
  mul() {
    return this.a * this.b;
  }
};

calculator.read();
alert(calculator.sum());
alert(calculator.mul());
```

<br>

### 3. Chaining (`ladder` object)

```js
let ladder = {
  step: 0,
  up() {
    this.step++;
    return this; // return the object for chaining
  },
  down() {
    this.step--;
    return this;
  },
  showStep() {
    alert(this.step);
    return this;
  }
};

// Example usage:
ladder.up().up().down().showStep().down().showStep();
```

<br>

✅ That’s the essence:

* **Methods** = functions in objects.
* **`this`** = runtime object before dot.
* **Arrow functions** → no `this` of their own.
* **Tasks** covered with working solutions.
