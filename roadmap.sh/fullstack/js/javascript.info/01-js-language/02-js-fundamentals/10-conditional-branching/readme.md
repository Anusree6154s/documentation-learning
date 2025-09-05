

## 🔹 Conditional Branching in JavaScript (`if`, `else`, `?`)

### 1. **The `if` Statement**

* Syntax:

  ```js
  if (condition) {
    // code executes if condition is true
  }
  ```
* Example:

  ```js
  let year = prompt('In which year was ECMAScript-2015 published?', '');
  if (year == 2015) {
    alert('You are right!');
  }
  ```
* Use `{}` even for single-line statements → improves readability.

<br>

### 2. **Boolean Conversion in `if`**

* The condition inside `if (…)` is converted to **boolean**.
* **Falsy values:** `0`, `""`, `null`, `undefined`, `NaN`.
* **Truthy values:** everything else.
* Examples:

  ```js
  if (0) { ... } // never runs
  if (1) { ... } // always runs
  ```

<br>

### 3. **The `else` Clause**

* Runs when condition is falsy.

  ```js
  if (year == 2015) {
    alert("Correct!");
  } else {
    alert("Wrong!");
  }
  ```

<br>

### 4. **Multiple Conditions (`else if`)**

* Used for checking several variants.

  ```js
  if (year < 2015) {
    alert("Too early...");
  } else if (year > 2015) {
    alert("Too late");
  } else {
    alert("Exactly!");
  }
  ```

<br>

### 5. **The Conditional (`?`) Operator**

* Shorter way to assign values based on conditions.
* Syntax:

  ```js
  let result = condition ? value1 : value2;
  ```
* Example:

  ```js
  let accessAllowed = (age > 18) ? true : false;
  // same as:
  let accessAllowed = age > 18;
  ```

<br>

### 6. **Multiple `?` (Chained Conditions)**

* Can be used like `if…else if…else`.

  ```js
  let age = prompt('age?', 18);

  let message = (age < 3) ? 'Hi, baby!' :
                (age < 18) ? 'Hello!' :
                (age < 100) ? 'Greetings!' :
                'What an unusual age!';
  ```

<br>

### 7. **Non-traditional Use of `?`**

* Can directly run code instead of assigning a value (not recommended).

  ```js
  (company == 'Netscape') ?
     alert('Right!') : alert('Wrong.');
  ```
* Prefer `if…else` in this case → more readable.
