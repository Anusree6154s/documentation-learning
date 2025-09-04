

## 🔹 Promise API – 6 Static Methods

### 1. **`Promise.all(iterable)`**

* Runs multiple promises **in parallel**, waits until **all are fulfilled**.
* Returns a promise with an **array of results (in order)**.
* If **any promise rejects → immediately rejects**, ignoring others.
* Accepts non-promises → passed as values directly.
* Use case: “all or nothing” operations (e.g., load all resources before rendering).

<br>

### 2. **`Promise.allSettled(iterable)`**

* Runs multiple promises in parallel, waits for **all to settle** (fulfilled or rejected).
* Returns an array of result objects:

  * `{status: "fulfilled", value: result}`
  * `{status: "rejected", reason: error}`
* Useful when you want **results of all promises**, even if some fail.

<br>

### 3. **`Promise.race(iterable)`**

* Resolves/rejects as soon as the **first promise settles**.
* Result/error of the first settled promise becomes the outcome.
* Other promises are ignored after that.
* Use case: **timeout handling** (whichever finishes first wins).

<br>

### 4. **`Promise.any(iterable)`**

* Resolves as soon as the **first fulfilled promise** is ready.
* Ignores rejections until a fulfillment happens.
* If **all promises reject → rejects with `AggregateError`** containing all errors.
* Use case: **“first successful result wins”**.

<br>

### 5. **`Promise.resolve(value)`**

* Creates an already **resolved promise** with the given value.
* Same as:

  ```js
  new Promise(resolve => resolve(value));
  ```
* Ensures a function always returns a promise (consistency).

<br>

### 6. **`Promise.reject(error)`**

* Creates an already **rejected promise** with the given error.
* Same as:

  ```js
  new Promise((_, reject) => reject(error));
  ```
* Rarely used directly.

<br>

## 🔹 Quick Summary Table

| Method               | Behavior                                                              |
| <br><br><br><br><br><br>-- | <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br> |
| `Promise.all`        | Waits for **all fulfilled** → array of results, rejects if one fails. |
| `Promise.allSettled` | Waits for **all settled** → array of `{status, value/reason}`.        |
| `Promise.race`       | First settled (fulfilled/rejected) decides outcome.                   |
| `Promise.any`        | First fulfilled wins; if all reject → `AggregateError`.               |
| `Promise.resolve`    | Creates resolved promise with value.                                  |
| `Promise.reject`     | Creates rejected promise with error.                                  |


