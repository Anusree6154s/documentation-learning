
## 🔹 **Switch Statement in JavaScript**

* **Purpose** → Alternative to multiple `if..else` checks.
* **Syntax**:

  ```js
  switch(x) {
    case 'value1': 
      // if (x === 'value1')
      ...
      break;

    case 'value2':
      ...
      break;

    default:
      ...
      break;
  }
  ```
* **How it works**:

  * Compares `x` with each `case` using **strict equality (===)**.
  * Runs the matched case until `break`.
  * If no match → runs `default` (if present).

---

### 🔸 Key Points

1. **Break is important** → Without it, execution continues to the next case.

   ```js
   switch(a) {
     case 3: alert("Too small"); // no break
     case 4: alert("Exactly!");  // executed too
   }
   ```

2. **Any expression allowed** in `switch` or `case`.

   ```js
   switch(+a) {
     case b + 1: alert("runs!"); break;
   }
   ```

3. <mark>**Grouping cases** → Cases can share the same code:</mark>

   ```js
   switch(a) {
     case 3:
     case 5:
       alert("Wrong!");
       break;
   }
   ```

4. **Strict equality (===)** → Type must match.

   * `case '3'` ≠ `case 3`
