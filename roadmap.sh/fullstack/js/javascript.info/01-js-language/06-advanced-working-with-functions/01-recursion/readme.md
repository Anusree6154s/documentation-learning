

## **Recursion & Stack – Key Points**

* **Recursion** → when a function calls itself.
* Useful when:

  * Task splits naturally into smaller tasks of the same kind.
  * Recursive data structures (trees, lists, nested objects).

<br>

### **Two Ways of Thinking**

* **Iterative** → use loops.
* **Recursive** → base case + recursive step.
* Example: `pow(x, n)`

  * Base: `pow(x, 1) = x`
  * Recursive: `pow(x, n) = x * pow(x, n-1)`
* **Recursion depth** = number of nested calls. Limited by JS engine (\~10,000).

<br>

### **Execution Context & Stack**

* Each function call has its own **execution context** (variables, flow, `this`, etc.).
* When a nested call is made:

  1. Current context → saved in **stack**.
  2. New context → created for subcall.
  3. After subcall finishes → old context restored.
* **Recursion depth = max number of contexts in stack.**
* Iterative versions usually use less memory.

<br>

### **Recursive Traversal**

* Example: company salary summation.
* Base case → array of employees → sum directly.
* Recursive step → object with subdepartments → recurse into each.
* Great for nested objects, trees, HTML/XML.

<br>

### **Recursive Structures**

* **Recursive data structure** → defined using itself.

  * Example: Linked list (`{ value, next -> list }`).
  * Trees (HTML DOM, org charts).
* **Linked List** vs Array:

  * Fast insert/delete anywhere (just rewire `next`).
  * Slow random access (must traverse).
  * Arrays are better for indexing, lists for queues/deques.

<br>

## **Tasks & Solutions**

### 1. **Sum all numbers till n**

```js
// Loop
function sumTo(n) {
  let sum = 0;
  for (let i = 1; i <= n; i++) sum += i;
  return sum;
}

// Recursion
function sumTo(n) {
  return n == 1 ? 1 : n + sumTo(n - 1);
}

// Formula
function sumTo(n) {
  return n * (n + 1) / 2;
}
```

* ✅ Fastest → Formula.
* ❌ Slowest → Recursion (too many calls).
* Cannot recurse with `n = 100000` → stack overflow.

<br>

### 2. **Factorial**

```js
function factorial(n) {
  return n == 1 ? 1 : n * factorial(n - 1);
}

alert(factorial(5)); // 120
```

<br>

### 3. **Fibonacci (fast version)**

```js
// Iterative (fast)
function fib(n) {
  let a = 1, b = 1;
  for (let i = 3; i <= n; i++) {
    let c = a + b;
    a = b;
    b = c;
  }
  return b;
}

alert(fib(77)); // 5527939700884757
```

* Recursive naive version is too slow → exponential calls.

<br>

### 4. **Output Linked List**

```js
let list = {
  value: 1,
  next: { value: 2, next: { value: 3, next: { value: 4, next: null } } }
};

// Loop
function printList(list) {
  let node = list;
  while (node) {
    alert(node.value);
    node = node.next;
  }
}

// Recursion
function printList(list) {
  alert(list.value);
  if (list.next) printList(list.next);
}
```

<br>

### 5. **Output Linked List in Reverse**

```js
// Recursion
function printReverseList(list) {
  if (list.next) printReverseList(list.next);
  alert(list.value);
}

// Loop
function printReverseList(list) {
  let arr = [];
  let node = list;
  while (node) {
    arr.push(node.value);
    node = node.next;
  }
  for (let i = arr.length - 1; i >= 0; i--) alert(arr[i]);
}
```

<br>

✅ **Summary**

* Recursion = elegant but memory-heavy (stack depth).
* Iterative solutions = more efficient, but sometimes harder to write.
* Recursive structures (trees, linked lists) are natural fits for recursion.
