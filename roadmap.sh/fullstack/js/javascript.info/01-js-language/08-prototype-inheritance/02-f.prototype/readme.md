
## 🔹 Key Ideas about `F.prototype`

1. `F.prototype` is a **regular property** of a constructor function.

   * But when we call `new F()`, JavaScript uses it to set the new object’s **\[\[Prototype]]**.

2. If you later change `F.prototype = somethingElse`, this only affects **future objects** created with `new F()`.

   * Existing ones keep their old `[[Prototype]]`.

3. By default every function has:

   ```js
   F.prototype = { constructor: F }
   ```

   So, objects created by `new F()` inherit a `constructor` property pointing back to `F`.

4. If you **overwrite** `F.prototype` completely, you lose the default `constructor` unless you manually restore it.

<br>

## 🔹 Tasks & Answers

### 1. Changing `prototype`

```js
function Rabbit() {}
Rabbit.prototype = { eats: true };

let rabbit = new Rabbit();

Rabbit.prototype = {};
alert(rabbit.eats);
```

✅ Output: **true**

* `rabbit`’s `[[Prototype]]` was already set to `{ eats: true }`.
* Later reassignment of `Rabbit.prototype` doesn’t affect existing objects.

<br>

```js
function Rabbit() {}
Rabbit.prototype = { eats: true };

let rabbit = new Rabbit();

Rabbit.prototype.eats = false;
alert(rabbit.eats);
```

✅ Output: **false**

* Both `rabbit.__proto__` and `Rabbit.prototype` point to the same object.
* Changing `eats` inside it affects `rabbit`.

<br>

```js
function Rabbit() {}
Rabbit.prototype = { eats: true };

let rabbit = new Rabbit();

delete rabbit.eats;
alert(rabbit.eats);
```

✅ Output: **true**

* `rabbit` has no own property `eats`.
* Deletion does nothing, lookup goes to prototype → `true`.

<br>

```js
function Rabbit() {}
Rabbit.prototype = { eats: true };

let rabbit = new Rabbit();

delete Rabbit.prototype.eats;
alert(rabbit.eats);
```

✅ Output: **undefined**

* `eats` is deleted from prototype object.
* Nothing to inherit → `undefined`.

<br>

### 2. Creating an object with the same constructor

```js
let obj2 = new obj.constructor();
```

* ✅ Works **if the prototype’s constructor points correctly** (default case or fixed manually):

  ```js
  function Rabbit(name) {
    this.name = name;
  }
  let obj = new Rabbit("White");
  let obj2 = new obj.constructor("Black");
  alert(obj2.name); // Black
  ```

* ❌ Fails **if prototype was overwritten without fixing `constructor`**:

  ```js
  function Rabbit(name) {
    this.name = name;
  }
  Rabbit.prototype = {}; // lost "constructor"

  let obj = new Rabbit("White");
  let obj2 = new obj.constructor("Black"); // Error, obj.constructor === Object
  ```

<br>

## 🔹 Summary Points

* `F.prototype` matters **only at `new F()` time**.
* Changing `F.prototype` later → affects only future instances.
* Default: `F.prototype = { constructor: F }`.
* If overwriting prototype, manually restore `constructor`.
* Existing objects keep their prototype even if `F.prototype` changes.
