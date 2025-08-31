

## 📌 Arrays in JavaScript

### Basics

* Arrays store **ordered collections** of values.
* Declaring arrays:

  ```js
  let arr = [];           // preferred
  let arr = new Array();  // rarely used
  ```
* Elements are accessed by index (`arr[0]`, `arr[1]` …), starting at **0**.
* `arr.length` → gives total elements (largest index + 1).
* Arrays can store **mixed types**: numbers, strings, objects, functions.

<br>

### Accessing Elements

* `arr[i]` → direct access.
* `arr.at(-1)` → last element (newer syntax, allows negative index).

<br>

### Modifying Arrays

* Replace: `arr[1] = "New"`.
* Add: `arr.push("Last")`, `arr.unshift("First")`.
* Remove: `arr.pop()` (last), `arr.shift()` (first).

<br>

### Queue vs Stack

* **Queue (FIFO):** `push` (end), `shift` (front).
* **Stack (LIFO):** `push` (end), `pop` (end).
* Arrays can work as **deque** (both ends).

<br>

### Performance

* `push` / `pop` → **fast** (work at end).
* `shift` / `unshift` → **slow** (must reindex).

<br>

### Loops

* `for (let i=0; i<arr.length; i++)` → classic, fast.
* `for (let item of arr)` → modern, clean.
* `for (let key in arr)` → ❌ bad for arrays (iterates properties, slow).

<br>

### Special Properties

* `length` auto-updates.
* Shortening length truncates:

  ```js
  let arr = [1,2,3,4];
  arr.length = 2; // [1,2]
  ```
* `arr.length = 0;` → quick way to clear array.

<br>

### Multi-dimensional Arrays

* Arrays can contain arrays (matrix):

  ```js
  let matrix = [[1,2,3],[4,5,6],[7,8,9]];
  console.log(matrix[0][1]); // 2
  ```

<br>

### Conversion & Comparison

* `arr.toString()` → comma-separated string.
* Adding arrays to strings triggers string conversion:

  * `[] + 1` → `"1"`
  * `[1] + 1` → `"11"`
* Arrays are objects → compared by **reference**:

  ```js
  [] == [] // false
  arr1 === arr2 // only true if same reference
  ```

<br>

## 📌 Tasks & Solutions

### 1. **Is array copied?**

```js
let fruits = ["Apples", "Pear", "Orange"];
let shoppingCart = fruits;
shoppingCart.push("Banana");
alert(fruits.length); // 4
```

➡ Arrays are copied **by reference**, both point to same object.

<br>

### 2. **Array operations**

```js
let styles = ["Jazz", "Blues"];
styles.push("Rock-n-Roll");
styles[Math.floor(styles.length/2)] = "Classics";
alert(styles.shift());
styles.unshift("Rap", "Reggae");
```

➡ Final: `["Rap", "Reggae", "Classics", "Rock-n-Roll"]`

<br>

### 3. **Calling in array context**

```js
let arr = ["a", "b"];
arr.push(function() { alert(this); });
arr[2](); // alerts ["a","b",function]
```

➡ `this` refers to the array itself.

<br>

### 4. **Sum input numbers**

```js
function sumInput() {
  let numbers = [];
  while (true) {
    let value = prompt("Enter number", "");
    if (value === "" || value === null || !isFinite(value)) break;
    numbers.push(+value);
  }
  return numbers.reduce((a, b) => a + b, 0);
}
```

<br>

### 5. **Maximal subarray (Kadane’s Algorithm, O(n))**

```js
function getMaxSubSum(arr) {
  let maxSum = 0, partialSum = 0;
  for (let item of arr) {
    partialSum = Math.max(0, partialSum + item);
    maxSum = Math.max(maxSum, partialSum);
  }
  return maxSum;
}
```

Examples:

* `getMaxSubSum([-1,2,3,-9]) → 5`
* `getMaxSubSum([-1,-2,-3]) → 0`
