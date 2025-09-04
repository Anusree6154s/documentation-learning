
## 🔹 Generators Overview

* Regular functions → return **one single value** (or nothing).
* Generators → can **yield multiple values on demand**.
* Declared with `function*` syntax.
* Calling a generator function does not run it immediately → it returns a **generator object**.

<br>

## 🔹 Generator basics

* Main method: `next()`.
* `next()` returns `{ value, done }`.

  * `value`: yielded value.
  * `done`: `true` if function finished.

```js
function* gen() {
  yield 1;
  yield 2;
  return 3;
}
let g = gen();
g.next(); // { value: 1, done: false }
g.next(); // { value: 2, done: false }
g.next(); // { value: 3, done: true }
```

<br>

## 🔹 Iterability

* Generators are **iterable** → work with `for..of`, spread `...`, etc.
* `for..of` ignores the final `return` value (when `done: true`).

```js
function* gen() {
  yield 1; yield 2; yield 3;
}
[...gen()]; // [1, 2, 3]
```

<br>

## 🔹 Generators for iterables

* You can replace `[Symbol.iterator]` with a generator for simpler code.

```js
let range = {
  from: 1, to: 5,
  *[Symbol.iterator]() {
    for (let i = this.from; i <= this.to; i++) yield i;
  }
};
[...range]; // [1,2,3,4,5]
```

<br>

## 🔹 Infinite generators

* Generators can yield **infinite values**.
* Must use `break` or other stopping logic in `for..of`.

<br>

## 🔹 Generator composition

* `yield*` delegates to another generator.

```js
function* genSeq(start, end) {
  for (let i = start; i <= end; i++) yield i;
}

function* genPasswordCodes() {
  yield* genSeq(48, 57);  // 0–9
  yield* genSeq(65, 90);  // A–Z
  yield* genSeq(97, 122); // a–z
}
```

<br>

## 🔹 Two-way communication

* `yield` can both:

  1. Return value outwards.
  2. Receive value inwards via `next(value)`.

```js
function* gen() {
  let x = yield "2 + 2 = ?";
  console.log(x); // 4 (from next(4))
}
let g = gen();
console.log(g.next().value); // "2 + 2 = ?"
g.next(4);
```

<br>

## 🔹 Error handling with `throw`

* You can inject an error into generator using `.throw(err)`.

```js
function* gen() {
  try {
    yield "Q?";
  } catch (e) {
    console.log("Error:", e.message);
  }
}
let g = gen();
g.next();
g.throw(new Error("Bad input"));
```

<br>

## 🔹 Stopping with `return`

* `generator.return(value)` → stops generator, returns `{ value, done: true }`.

```js
function* gen() {
  yield 1; yield 2;
}
let g = gen();
g.return("end"); // { value: "end", done: true }
```

<br>

## 🔹 Summary

* Defined with `function*`.
* Use `yield` to return values step by step.
* Generators are iterable (`for..of`, spread).
* Can be infinite.
* Support **composition (`yield*`)**.
* Support **two-way communication** (`next(value)`).
* Can handle errors with `.throw()` and stop with `.return()`.

<br>

## 📝 Task: Pseudo-random generator (solution)

```js
function* pseudoRandom(seed) {
  let value = seed;
  while (true) {
    value = value * 16807 % 2147483647;
    yield value;
  }
}

// Example usage
let generator = pseudoRandom(1);
console.log(generator.next().value); // 16807
console.log(generator.next().value); // 282475249
console.log(generator.next().value); // 1622650073
```
