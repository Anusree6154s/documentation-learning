

### 🔹 Types of Object Properties

1. **Data properties** → store a value directly (normal properties).
2. **Accessor properties** → defined with **get** and **set** methods; they look like normal properties but execute functions behind the scenes.

<br>

### 🔹 Getters and Setters

* **Getter** → runs when the property is read.
* **Setter** → runs when the property is assigned a value.

Example:

```js
let user = {
  name: "John",
  surname: "Smith",

  get fullName() {
    return `${this.name} ${this.surname}`;
  },

  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  }
};

alert(user.fullName); // John Smith
user.fullName = "Alice Cooper"; 
alert(user.name); // Alice
```

<br>

### 🔹 Accessor Descriptors (`Object.defineProperty`)

* Accessor properties use `get` and `set` instead of `value` and `writable`.
* Descriptor options:

  * `get` → function without args, triggered on read.
  * `set` → function with one arg, triggered on write.
  * `enumerable` → whether property shows up in `for...in`.
  * `configurable` → whether property can be changed/deleted.

Example:

```js
Object.defineProperty(user, 'fullName', {
  get() { return `${this.name} ${this.surname}`; },
  set(value) { [this.name, this.surname] = value.split(" "); }
});
```

⚠️ A property can be either a **data property** OR an **accessor property**, not both.
Mixing `get` with `value` causes an error.

<br>

### 🔹 Smarter Getters/Setters (Validation)

* Can add control over values.
* Convention: use **`_property`** for internal storage.

Example:

```js
let user = {
  get name() { return this._name; },
  set name(value) {
    if (value.length < 4) {
      alert("Name is too short");
      return;
    }
    this._name = value;
  }
};

user.name = "Pete"; // works
user.name = ""; // blocked
```

<br>

### 🔹 Using for Compatibility

* Useful when data model changes but you want to keep old code working.
* Example: replacing `age` with `birthday` but still supporting `age`:

```js
function User(name, birthday) {
  this.name = name;
  this.birthday = birthday;

  Object.defineProperty(this, "age", {
    get() {
      let todayYear = new Date().getFullYear();
      return todayYear - this.birthday.getFullYear();
    }
  });
}

let john = new User("John", new Date(1992, 6, 1));
alert(john.age); // still works
```

<br>

✅ **Summary:**

* `get` → compute property on access.
* `set` → handle property assignment.
* Defined inside object literals or with `Object.defineProperty`.
* Great for **virtual properties**, **validation**, and **backward compatibility**.
