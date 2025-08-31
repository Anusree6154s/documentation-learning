

## 🔹 Objects in JavaScript

* **Primitive types** = 7 simple types (string, number, boolean, null, undefined, bigint, symbol).
* **Objects** = key-value collections (complex data structures).
* Think of objects like a **cabinet with files** (keys = labels, values = contents).

### Ways to Create:

* `let user = new Object();` // constructor syntax
* `let user = {};` // literal syntax (common)

### Properties:

* Written as `key: value`.
* Keys are strings (or symbols), values can be anything.
* Example:

  ```js
  let user = { name: "John", age: 30 };
  ```

### Accessing Properties:

* **Dot notation**: `user.name`
* **Square brackets**: `user["likes birds"]` (needed if key has spaces or is dynamic).
* Dynamic key example:

  ```js
  let key = "age";
  console.log(user[key]);
  ```

### Adding / Removing:

* Add: `user.isAdmin = true`
* Delete: `delete user.age`

### Computed Properties:

* Key can come from a variable/expression.

  ```js
  let fruit = "apple";
  let bag = { [fruit]: 5 }; // { apple: 5 }
  ```

### Property Value Shorthand:

* If variable name = property name:

  ```js
  function makeUser(name, age) {
    return { name, age };
  }
  ```

### Property Names:

* No restriction (can use reserved words).
* Numbers are auto-converted to strings.
* Special case: `__proto__` behaves differently.

### Checking Existence:

* `obj.noSuchProp === undefined`
* `"key" in obj` (more reliable when value could be `undefined`)

### Iteration:

* `for (let key in obj)` → loops over all keys.
* Values via `obj[key]`.

### Order of Properties:

* **Integer keys** → sorted ascending.
* **Non-integer keys** → in creation order.

<br>

## 🔹 Tasks

### 1. Hello, object

```js
let user = {}; 
user.name = "John"; 
user.surname = "Smith"; 
user.name = "Pete"; 
delete user.name;
```

### 2. Check for emptiness

```js
function isEmpty(obj) {
  for (let key in obj) return false;
  return true;
}
```

### 3. Sum object properties

```js
let salaries = { John: 100, Ann: 160, Pete: 130 };
let sum = 0;
for (let key in salaries) sum += salaries[key];
console.log(sum); // 390
```

### 4. Multiply numeric property values

```js
function multiplyNumeric(obj) {
  for (let key in obj) {
    if (typeof obj[key] === "number") {
      obj[key] *= 2;
    }
  }
}
```