

### Arrow Functions – Basics

* Syntax:

  ```js
  let func = (arg1, arg2, ..., argN) => expression;
  ```
* Shorter form of:

  ```js
  let func = function(arg1, arg2, ..., argN) {
    return expression;
  };
  ```

<br>

### Examples

1. **Two arguments**

   ```js
   let sum = (a, b) => a + b;
   alert(sum(1, 2)); // 3
   ```

2. **Single argument (parentheses optional)**

   ```js
   let double = n => n * 2;
   alert(double(3)); // 6
   ```

3. **No arguments (must use parentheses)**

   ```js
   let sayHi = () => alert("Hello!");
   sayHi();
   ```

4. **Conditional function assignment**

   ```js
   let age = prompt("What is your age?", 18);
   let welcome = (age < 18) ?
     () => alert("Hello!") :
     () => alert("Greetings!");
   welcome();
   ```

<br>

### Multiline Arrow Functions

* Use `{ }` for multiple statements.
* Must explicitly `return` a value.

  ```js
  let sum = (a, b) => {
    let result = a + b;
    return result;
  };
  alert(sum(1, 2)); // 3
  ```

<br>

### Summary

* **Without braces**: one expression, auto-return.
* **With braces**: multiple statements, need explicit `return`.
* Useful for one-liners and callbacks.
