
## 📌 Object.keys / Object.values / Object.entries

### 1. What they do

* **`Object.keys(obj)`** → array of keys
* **`Object.values(obj)`** → array of values
* **`Object.entries(obj)`** → array of `[key, value]` pairs

```js
let user = { name: "John", age: 30 };

Object.keys(user);   // ["name", "age"]
Object.values(user); // ["John", 30]
Object.entries(user);// [["name","John"], ["age",30]]
```

<br>

### 2. Difference from Map

| Feature     | `Map`        | `Object`           |
| ----------- |------------- | ------------------ |
| Syntax      | `map.keys()` | `Object.keys(obj)` |
| Return type | **Iterable** | **Real Array**     |

* Objects require calling `Object.*` functions.
* Arrays returned are “real” arrays (with map, filter, etc.).

<br>

### 3. Looping with values

```js
let user = { name: "John", age: 30 };

for (let value of Object.values(user)) {
  console.log(value); // John, 30
}
```

<br>

### 4. Symbol keys are ignored

* Like `for..in`, these methods **ignore `Symbol` properties**.
* To include them:

  * `Object.getOwnPropertySymbols(obj)` → only symbols
  * `Reflect.ownKeys(obj)` → all keys (string + symbols)

<br>

### 5. Transforming objects

* Objects lack array methods (`map`, `filter`, etc.).
* Workaround:

  1. `Object.entries(obj)` → array of pairs
  2. Apply array methods
  3. `Object.fromEntries(arr)` → back to object

#### Example: Double prices

```js
let prices = { banana: 1, orange: 2, meat: 4 };

let doublePrices = Object.fromEntries(
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);

console.log(doublePrices.meat); // 8
```

<br>

✅ **Summary**:

* Use `Object.keys/values/entries` for working with plain objects.
* They return real arrays (unlike Map’s iterables).
* Use `Object.entries` + `Object.fromEntries` to transform objects with array methods.
