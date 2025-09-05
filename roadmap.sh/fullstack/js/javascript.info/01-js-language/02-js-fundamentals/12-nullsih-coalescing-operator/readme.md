

## **Nullish Coalescing Operator (??)**

### **Basics**

* `a ?? b` → returns:

  * `a` if it’s **defined** (not `null` or `undefined`),
  * otherwise `b`.
* Equivalent to:

  ```js
  a !== null && a !== undefined ? a : b
  ```

<br>

### **Use Case**

* Provide **default values** when a variable is `null`/`undefined`.

  ```js
  let user;
  alert(user ?? "Anonymous"); // "Anonymous"

  let user = "John";
  alert(user ?? "Anonymous"); // "John"
  ```

<br>

### **Multiple Values**

* Picks the first **defined** value.

  ```js
  let firstName = null, lastName = null, nickName = "Supercoder";
  alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // "Supercoder"
  ```

<br>

### **?? vs ||**

* `||` → returns first **truthy** value.
* `??` → returns first **defined** value.
* Example:

  ```js
  let height = 0;
  alert(height || 100); // 100 (0 is falsy)
  alert(height ?? 100); // 0   (0 is defined)
  ```

<br>

### **Precedence**

* Precedence = `||` (low, value = 3).
* Evaluated before `=` and `?`, after `+`, `*`, etc.
* Use **parentheses**:

  ```js
  let area = (height ?? 100) * (width ?? 50);
  ```

<br>

### **Restrictions**

* Cannot mix `??` with `||` or `&&` **without parentheses**.

  ```js
  let x = (1 && 2) ?? 3; // valid → 2
  let x = 1 && 2 ?? 3;   // syntax error
  ```

<br>

### **Summary**

* `??` → choose the first **defined** value.
* Safer than `||` when valid values like `0`, `""`, or `false` should not be replaced.
* Low precedence → add parentheses in expressions.
* Disallowed directly with `||` or `&&` → wrap in parentheses.
