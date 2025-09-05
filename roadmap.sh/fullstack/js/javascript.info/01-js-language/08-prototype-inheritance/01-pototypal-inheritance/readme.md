
## 🔑 Prototypal Inheritance – Key Points

### 1. Basics

* Every object has a hidden property **`[[Prototype]]`** → references another object (or `null`).
* This object is called the **prototype**.
* If a property is missing in the object, JavaScript looks for it in the prototype chain.

<br>

### 2. Setting Prototypes

* Historical way: `obj.__proto__ = otherObj;`
* Modern way: `Object.getPrototypeOf(obj)` / `Object.setPrototypeOf(obj, proto)`.
* Prototypes form a **chain**, e.g. `longEar → rabbit → animal → Object.prototype → null`.

<br>

### 3. Read vs Write

* **Reading:** looks up the prototype chain.
* **Writing:** always writes directly to the object itself (unless a **setter** exists).
* Example:

  ```js
  rabbit.walk = function() { alert("Rabbit walk"); }
  rabbit.walk(); // Uses rabbit’s own, not animal’s
  ```

<br>

### 4. `this` Behavior

* `this` is **always the object before the dot**, not the prototype.
* Example:

  ```js
  rabbit.sleep(); // writes rabbit.isSleeping
  ```
* Methods are shared, but **state stays local**.

<br>

### 5. Accessor Properties

* Getters/setters in prototype **work with child objects** because `this` refers to the caller.
* Example: `admin.fullName = "Alice Cooper"` → modifies `admin`, not `user`.

<br>

### 6. Iteration

* **`for…in`** → iterates over own + inherited properties (enumerable only).
* **`Object.keys/values/entries`** → own properties only.
* `obj.hasOwnProperty(key)` → check if property belongs directly to object.

<br>

## 📝 Tasks & Solutions

### 1. Working with prototype

```js
let animal = { jumps: null };
let rabbit = { __proto__: animal, jumps: true };

alert(rabbit.jumps); // (1) true → own property
delete rabbit.jumps;
alert(rabbit.jumps); // (2) null → from animal
delete animal.jumps;
alert(rabbit.jumps); // (3) undefined → nothing found
```

✅ **Answers:** true, null, undefined

<br>

### 2. Searching algorithm

```js
let head = { glasses: 1 };
let table = { pen: 3, __proto__: head };
let bed = { sheet: 1, pillow: 2, __proto__: table };
let pockets = { money: 2000, __proto__: bed };

pockets.pen; // 3 (from table)
bed.glasses; // 1 (from head)
```

⚡ Performance: `pockets.glasses` vs `head.glasses` is the same speed.

* Prototype lookups are optimized internally.
* No need to worry about performance here.

<br>

### 3. Where does it write?

```js
let animal = {
  eat() { this.full = true; }
};
let rabbit = { __proto__: animal };

rabbit.eat();
```

✅ `rabbit.full = true` (not animal).
Because `this` is always the caller → here `rabbit`.

<br>

### 4. Why are both hamsters full?

```js
let hamster = {
  stomach: [],   // shared between all!
  eat(food) {
    this.stomach.push(food);
  }
};

let speedy = { __proto__: hamster };
let lazy = { __proto__: hamster };

speedy.eat("apple");
alert(speedy.stomach); // ["apple"]
alert(lazy.stomach);   // ["apple"] ❌
```

⚠️ Problem: `stomach` is defined **once in prototype**, so all share it.

✅ Fix: each hamster should have its own stomach:

```js
let hamster = {
  eat(food) {
    this.stomach.push(food);
  }
};

let speedy = { stomach: [], __proto__: hamster };
let lazy = { stomach: [], __proto__: hamster };
```

<br>

## ✅ Summary Recap

* **Prototype = fallback storage for properties/methods**.
* Reading climbs chain → writing goes local.
* `this` = caller object, not prototype.
* Iteration: `for..in` includes inherited, `Object.keys` doesn’t.
* Shared properties (like arrays/objects) in prototypes → dangerous (shared state bug).
