
## 🔹 Event Loop Basics

* JS engine runs tasks in a loop:

  1. Take oldest task from **macrotask queue**.
  2. Run it.
  3. After that, run **all microtasks**.
  4. Render updates.
  5. Wait for next task.
* Browser JS is **single-threaded**, idle until events/tasks appear.

<br>

## 🔹 Tasks (Macrotasks)

* Examples:

  * Script execution.
  * `setTimeout`, `setInterval`.
  * UI events (`onclick`, `mousemove`).
  * Network events (XHR, fetch).
* Processed **FIFO** (first in → first out).
* Rendering happens **after macrotask + microtasks** finish.
* Heavy macrotask blocks UI (e.g., infinite loop).

<br>

## 🔹 Splitting Heavy Work

* Instead of big blocking loop → split into chunks with `setTimeout(fn, 0)`.
* Each chunk runs, then event loop handles pending tasks (keeps UI responsive).
* Nested timers have min delay (\~4ms in browsers).

✅ Pattern:

```js
function bigTask() {
  if (notDone) setTimeout(bigTask);
  // do part of work
}
```

<br>

## 🔹 Progress Indication

* DOM changes **painted only after current task ends**.
* If job is split with `setTimeout`, progress can update gradually.

<br>

## 🔹 Postpone Actions

* Use `setTimeout(fn, 0)` inside event handler → runs after event fully bubbles.
* Example: dispatching custom event after click handling finished.

<br>

## 🔹 Microtasks

* Created by:

  * `Promise.then/catch/finally`.
  * `await`.
  * `queueMicrotask(fn)`.
* Run **after current macrotask completes**, before rendering or new macrotask.
* Run **all microtasks until empty** before moving on.
* Guarantee: app state is stable (no new user input/network in between).

<br>

## 🔹 Macrotasks vs Microtasks

* **Macrotask** → `setTimeout`, `setInterval`, UI events.
* **Microtask** → promises, `queueMicrotask`.
* Order of execution:

  1. Run sync code.
  2. Finish macrotask.
  3. Run all microtasks.
  4. Render.
  5. Take next macrotask.

<br>

## 🔹 Web Workers

* Run code in separate thread (parallel).
* Can’t access DOM.
* Communicate via messages.
* Best for CPU-heavy tasks.

<br>

## 🔹 Task Example

```js
console.log(1);

setTimeout(() => console.log(2));       // macrotask
Promise.resolve().then(() => console.log(3));   // microtask
Promise.resolve().then(() => setTimeout(() => console.log(4))); // microtask → macrotask
Promise.resolve().then(() => console.log(5));   // microtask
setTimeout(() => console.log(6));       // macrotask

console.log(7);
```

👉 **Execution order:**

1. `1` (sync)
2. `7` (sync)
3. `3` (microtask)
4. `5` (microtask)
5. `2` (macrotask)
6. `6` (macrotask)
7. `4` (macrotask, scheduled inside microtask)

✅ Final output:
`1, 7, 3, 5, 2, 6, 4`
