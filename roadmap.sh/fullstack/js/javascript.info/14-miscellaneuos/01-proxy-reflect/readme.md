
# 🔹 Proxy and Reflect – Summary

## 1. What is Proxy?

* `Proxy` = wrapper around a target object.
* Syntax:

  ```js
  let proxy = new Proxy(target, handler)
  ```

  * **target** → the real object.
  * **handler** → config object with “traps” (functions that intercept operations).
* If no trap is defined → all operations are transparently forwarded to the target.

<br>

## 2. Common Proxy Traps

| Internal Method       | Trap (Handler Method) | Triggers when…           |
| <br><br><br><br><br><br><br> | <br><br><br><br><br><br><br> | <br><br><br><br><br><br><br><br> |
| `[[Get]]`             | `get`                 | Reading a property       |
| `[[Set]]`             | `set`                 | Writing to a property    |
| `[[HasProperty]]`     | `has`                 | `in` operator            |
| `[[Delete]]`          | `deleteProperty`      | `delete` operator        |
| `[[Call]]`            | `apply`               | Function call            |
| `[[Construct]]`       | `construct`           | `new` operator           |
| `[[OwnPropertyKeys]]` | `ownKeys`             | `Object.keys`, `for..in` |
| `[[GetPrototypeOf]]`  | `getPrototypeOf`      | `Object.getPrototypeOf`  |
| ...                   | ...                   | many more                |

⚠️ Traps must respect **invariants** (rules from the JS spec). Example:

* `set` must return `true` if successful, otherwise `TypeError`.
* Prototype must always match the target’s prototype.

<br>

## 3. Examples of Proxy Use Cases

* **Default values with `get`**

  ```js
  let arr = new Proxy([0,1,2], {
    get(target, prop) {
      return prop in target ? target[prop] : 0;
    }
  });
  console.log(arr[123]); // 0
  ```

* **Validation with `set`**

  ```js
  let numbers = new Proxy([], {
    set(target, prop, val) {
      if (typeof val === "number") {
        target[prop] = val; return true;
      }
      return false; // TypeError
    }
  });
  ```

* **Filter keys with `ownKeys`**
  Hide private `_` keys from `Object.keys` / `for..in`.

* **Access protection (`get`, `set`, `deleteProperty`)**
  Block access to properties starting with `_`.

* **Custom `in` operator with `has`**
  Check if number lies in a range:

  ```js
  let range = new Proxy({start:1,end:10}, {
    has(t, p) { return p >= t.start && p <= t.end; }
  });
  console.log(5 in range); // true
  ```

* **Wrap functions with `apply`**
  Delay execution, logging, etc.

<br>

## 4. Reflect

* `Reflect` = built-in object mirroring Proxy traps.
* Provides methods: `Reflect.get`, `Reflect.set`, `Reflect.deleteProperty`, `Reflect.construct`, etc.
* Used to **forward** operations inside traps.

  ```js
  let user = new Proxy({name:"John"}, {
    get(t,p,r){ console.log("GET",p); return Reflect.get(t,p,r); },
    set(t,p,v,r){ console.log("SET",p,v); return Reflect.set(t,p,v,r); }
  });
  ```

✅ Benefit: handles tricky cases like getters/setters with correct `this` (`receiver`).

<br>

## 5. Proxy Limitations

* Built-in objects (`Map`, `Set`, `Date`, etc.) use **internal slots** → proxies can break them.

  * Workaround: bind methods to the target inside `get`.
* Private class fields (`#field`) also use internal slots → break after proxying.
* Proxy and target are different objects → strict equality `===` cannot be intercepted.
* Performance overhead: property access via Proxy is slower (several times).

<br>

## 6. Revocable Proxy

* Syntax:

  ```js
  let {proxy, revoke} = Proxy.revocable(target, handler);
  revoke(); // disables proxy
  ```
* Useful for **temporary access** to objects.

<br>

## 7. Tasks (with Solutions)

### (a) Error on non-existent property

```js
function wrap(target) {
  return new Proxy(target, {
    get(t, prop) {
      if (prop in t) return t[prop];
      throw new ReferenceError(`Property doesn't exist: "${prop}"`);
    }
  });
}
```

### (b) Array negative indexes

```js
let array = new Proxy([1,2,3], {
  get(t, prop) {
    if (prop < 0) prop = t.length + Number(prop);
    return t[prop];
  }
});
```

### (c) Observable object

```js
function makeObservable(target) {
  let handlers = [];
  return new Proxy(target, {
    set(t, prop, val, r) {
      t[prop] = val;
      handlers.forEach(h => h(prop, val));
      return true;
    },
    get(t, prop, r) {
      if (prop === "observe") {
        return fn => handlers.push(fn);
      }
      return Reflect.get(t, prop, r);
    }
  });
}
```

<br>

✅ **Summary**:

* `Proxy` lets you **intercept and customize** fundamental object operations.
* `Reflect` provides a safe way to forward operations.
* Use cases: **default values, validation, security, custom operators, function decorators, observables**.
* Limitations: internal slots, private fields, `===`, performance.
