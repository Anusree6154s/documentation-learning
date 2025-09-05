
## 🔑 Key Points about WeakMap & WeakSet

* **WeakMap**

  * Keys must be **objects**.
  * Values can be **anything**.
  * Keys/values are **removed automatically** when the object is no longer referenced elsewhere (garbage collection).
  * Methods: `set`, `get`, `delete`, `has`.
  * No iteration (`keys`, `values`, `entries` not available).
  * Use case: attach **extra data** to objects without preventing GC.

* **WeakSet**

  * Only stores **objects** (no primitives).
  * Keeps object in the set only while it’s reachable elsewhere.
  * Methods: `add`, `has`, `delete`.
  * No `size`, no iteration.
  * Use case: track **yes/no facts** about objects.

* **Why use them?**

  * Prevent **memory leaks**.
  * Perfect for “secondary” info tied to the lifecycle of objects.

<br>

## 📝 Task 1: Store "unread" flags

### Problem

We need to track if a **message** has been read.

* ✅ Must disappear automatically when message is deleted.
* ❌ Cannot modify the message object itself.

### ✅ Solution

Use **WeakSet**, since it’s just a “yes/no” flag.

```js
let messages = [
  {text: "Hello", from: "John"},
  {text: "How goes?", from: "John"},
  {text: "See you soon", from: "Alice"}
];

let readMessages = new WeakSet();

// mark some messages as read
readMessages.add(messages[0]); 
readMessages.add(messages[1]);

console.log(readMessages.has(messages[0])); // true
console.log(readMessages.has(messages[2])); // false

messages.shift(); // remove first message
// now readMessages also loses it automatically
```

<br>

## 📝 Task 2: Store read dates

### Problem

We want to know **when** a message was read.

* ✅ Should also disappear automatically when message is deleted.

### ✅ Solution

Use **WeakMap**, since we need to store extra data (a `Date`).

```js
let messages = [
  {text: "Hello", from: "John"},
  {text: "How goes?", from: "John"},
  {text: "See you soon", from: "Alice"}
];

let readDates = new WeakMap();

// set read time
readDates.set(messages[0], new Date(2025, 7, 31));
readDates.set(messages[1], new Date());

console.log(readDates.get(messages[0])); // date object
console.log(readDates.get(messages[2])); // undefined

messages.shift(); 
// readDates entry is cleaned up automatically
```

<br>

## 📌 Summary

* **WeakSet** → for simple **yes/no facts** tied to objects.
* **WeakMap** → for storing **extra info** (e.g., timestamps, metadata).
* Both auto-clean when objects are garbage collected → ✅ no memory leaks.
