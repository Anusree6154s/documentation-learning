

## ⏰ Scheduling in JavaScript – `setTimeout` & `setInterval`

### 1. Purpose
- **`setTimeout(func, delay)`** → runs a function **once** after `delay` ms.  
- **`setInterval(func, delay)`** → runs a function **repeatedly** every `delay` ms.

<br>

### 2. Syntax
```js
let timerId = setTimeout(func | code, [delay], [arg1], [arg2], ...);
let timerId = setInterval(func | code, [delay], [arg1], [arg2], ...);
```

<br>

### 3. Examples
✅ Run once:
```js
function sayHi() {
  alert("Hello");
}
setTimeout(sayHi, 1000); // after 1 second
```

✅ With arguments:
```js
function greet(phrase, who) {
  alert(`${phrase}, ${who}`);
}
setTimeout(greet, 1000, "Hello", "John"); // Hello, John
```

✅ Cancel scheduled call:
```js
let timerId = setTimeout(() => alert("Never happens"), 1000);
clearTimeout(timerId);
```

✅ Repeatedly with `setInterval`:
```js
let timerId = setInterval(() => alert("tick"), 2000);
setTimeout(() => clearInterval(timerId), 5000); // stop after 5s
```

<br>

### 4. Nested `setTimeout` (flexible alternative to `setInterval`)
```js
let timerId = setTimeout(function tick() {
  alert("tick");
  timerId = setTimeout(tick, 2000); // schedules next after previous finishes
}, 2000);
```
- Better than `setInterval` when execution time varies.  
- Guarantees fixed delay **between calls**, not overlapping.

<br>

### 5. Zero-delay `setTimeout`
```js
setTimeout(() => alert("World"));
alert("Hello");
```
➡️ Always prints **Hello → World** (even if delay is `0`, it runs after current script finishes).

⚠️ Browser enforces **minimum 4ms delay** after 5 nested calls.

<br>

### 6. Garbage Collection Note
- Functions scheduled with timers are kept in memory.  
- Cancel unused timers to free memory.

<br>

### 7. Tasks / Exercises

#### (a) Print numbers every second (2 ways)

**Using `setInterval`:**
```js
function printNumbers(from, to) {
  let current = from;
  let timerId = setInterval(() => {
    console.log(current);
    if (current === to) clearInterval(timerId);
    current++;
  }, 1000);
}

printNumbers(1, 5);
```

**Using nested `setTimeout`:**
```js
function printNumbers(from, to) {
  let current = from;

  setTimeout(function go() {
    console.log(current);
    if (current < to) setTimeout(go, 1000);
    current++;
  }, 1000);
}

printNumbers(1, 5);
```

<br>

#### (b) What will `setTimeout` show?
```js
let i = 0;

setTimeout(() => alert(i), 100); // ?

// heavy loop >100ms
for (let j = 0; j < 100000000; j++) {
  i++;
}
```
👉 The callback runs **after the loop finishes**, so it shows the **final value of `i`**.  
Because timers **wait until current script finishes**.

<br>

✅ **Summary**
- Use `setTimeout` for delayed execution (once).  
- Use `setInterval` for repeated execution, but prefer **nested `setTimeout`** for flexible scheduling.  
- Timers don’t interrupt code → they wait until the current execution finishes.  
- Zero-delay is not truly zero → executes after current code.  
