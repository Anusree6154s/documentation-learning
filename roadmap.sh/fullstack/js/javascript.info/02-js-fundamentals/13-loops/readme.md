

## 🔁 Loops in JavaScript

* Loops → allow repeating code multiple times.
* Types covered: **while, do..while, for**.
* Other loops: **for…in (object props)**, **for…of (arrays/iterables)**.

<br>

### 1. **while loop**

* Syntax:

  ```js
  while (condition) { body }
  ```
* Runs as long as condition is truthy.
* Example:

  ```js
  let i = 0;
  while (i < 3) { alert(i); i++; } // 0,1,2
  ```
* Can omit `{}` for single-line body.
* Condition can be any truthy/falsy expression.

<br>

### 2. **do…while loop**

* Runs body **at least once**, then checks condition.
* Syntax:

  ```js
  do { body } while (condition);
  ```
* Example:

  ```js
  let i = 0;
  do { alert(i++); } while (i < 3); // 0,1,2
  ```

<br>

### 3. **for loop**

* Syntax:

  ```js
  for (begin; condition; step) { body }
  ```
* Example:

  ```js
  for (let i=0; i<3; i++) alert(i); // 0,1,2
  ```
* Parts:

  * **begin** → run once at start.
  * **condition** → checked each iteration.
  * **step** → runs after body each time.
* Can skip any part (`for(; condition ;)`).
* `for(;;)` → infinite loop.

<br>

### 4. **Breaking / Continuing**

* **break** → exit loop immediately.
* **continue** → skip current iteration, go to next.
* Useful to filter values (e.g., skip evens).

<br>

### 5. <mark>**Labels**</mark>

* Allow breaking/continuing **outer loops**.
* Example:

  ```js
  outer: for (let i=0; i<3; i++) {
    for (let j=0; j<3; j++) {
      if (!prompt(...)) break outer;
    }
  }
  alert("Done");
  ```

<br>

### 6. **Summary**

* `while` → condition checked before body.
* `do…while` → body runs at least once.
* `for` → compact, all in one line.
* Infinite loop → `while(true)` or `for(;;)`.
* Use **break** to stop, **continue** to skip.
* **Labels** → break/continue out of nested loops.

<br>

## 📝 Tasks (Practice)

1. **Last loop value**

   ```js
   let i=3; while(i) alert(i--);
   ```

   → Last shown: **1**.

2. **Prefix vs Postfix in while**

   ```js
   let i=0; while (++i < 5) alert(i); // 1..4
   let i=0; while (i++ < 5) alert(i); // 1..5
   ```

3. **Prefix vs Postfix in for**

   ```js
   for (let i=0; i<5; i++) alert(i);   // 0..4
   for (let i=0; i<5; ++i) alert(i);   // 0..4 (same)
   ```

4. **Even numbers 2–10**

   ```js
   for (let i=2; i<=10; i+=2) alert(i);
   ```

5. **Replace for with while**

   ```js
   let i=0;
   while (i<3) { alert(`number ${i}!`); i++; }
   ```

6. **Prompt >100**

   ```js
   let num;
   do {
     num = prompt("Enter number > 100");
   } while (num <= 100 && num);
   ```

7. **Primes up to n**

   ```js
   let n = 10;
   for (let i=2; i<=n; i++) {
     let prime = true;
     for (let j=2; j<i; j++) {
       if (i % j === 0) { prime=false; break; }
     }
     if (prime) alert(i);
   }
   // 2,3,5,7
   ```