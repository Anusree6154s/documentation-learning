

### 📌 Regular Iterables Recap

* Objects can be made iterable using **`Symbol.iterator`**.
* `next()` returns `{ done: true/false, value }`.
* Used with `for..of`.

<br>

### 📌 Async Iterables

* Used when values arrive asynchronously (e.g., network, timers).
* Implemented using **`Symbol.asyncIterator`**.
* `next()` must return a **Promise**.
* Iterated with **`for await..of`**.

Example: values `1..5` with 1s delay.

<br>

### 📌 Differences: Iterators vs Async Iterators

| Feature        | Iterators (`Symbol.iterator`) | Async Iterators (`Symbol.asyncIterator`) |
| -------------- | ----------------------------- | ---------------------------------------- |
| `next()` value | Any value                     | **Promise** resolving to value           |
| Loop syntax    | `for..of`                     | `for await..of`                          |
| Spread syntax  | ✅ Works                       | ❌ Doesn’t work                           |

<br>

### 📌 Generators Recap

* Defined with `function*`.
* Use `yield` to generate values step by step.
* Shorter, cleaner syntax for creating iterables.

<br>

### 📌 Async Generators

* Defined with **`async function*`**.
* Can use **`await` inside**.
* Each `generator.next()` returns a **Promise**.
* Iterated with `for await..of`.

Example: yield numbers `1..5` with async delay.

<br>

### 📌 Async Generators as Async Iterables

* Can use async generators directly in **`Symbol.asyncIterator`**.
* Makes objects asynchronously iterable.

<br>

### 📌 Real-Life Example: Paginated API (GitHub commits)

* API returns data in **pages** (e.g., 30 commits per request).
* Async generator fetches page → yields commits one by one → continues with next page.
* Usage:

  ```js
  for await (let commit of fetchCommits("user/repo")) {
    console.log(commit);
  }
  ```

<br>

### 📌 Summary

* **Regular iterators/generators** → sync data.
* **Async iterators/generators** → async data with delays or network.
* **Syntax differences**:

| Generators   | Async Generators  |                           |
| ------------ | ----------------- | ------------------------- |
| `function*`  | `async function*` |                           |
| Return value | `{value, done}`   | Promise → `{value, done}` |
| Loop         | `for..of`         | `for await..of`           |

* Common in streams, paginated APIs, and big file transfers.
