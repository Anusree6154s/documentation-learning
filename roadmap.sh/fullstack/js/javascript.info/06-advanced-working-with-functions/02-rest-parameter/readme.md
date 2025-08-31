

### 📌 Rest Parameters

* Functions in JS can be called with **any number of arguments**, even if defined with fewer parameters.
* **Rest parameters** (`...args`) gather all extra arguments into an array.

  ```js
  function sumAll(...args) {
    return args.reduce((a, b) => a + b, 0);
  }
  console.log(sumAll(1, 2, 3, 4)); // 10
  ```
* You can mix normal parameters with rest:

  ```js
  function showName(firstName, lastName, ...titles) {
    console.log(firstName, lastName, titles);
  }
  showName("Julius", "Caesar", "Consul", "Imperator");
  ```
* ❌ Rest must always be **last** in the parameter list:

  ```js
  function f(arg1, ...rest, arg2) { } // ❌ Error
  ```

<br>

### 📌 `arguments` Object

* Special array-like object that contains all arguments.
* Example:

  ```js
  function showName() {
    console.log(arguments.length, arguments[0], arguments[1]);
  }
  showName("Julius", "Caesar"); // 2, Julius, Caesar
  ```
* Limitations:

  * Not a real array (no `.map`, `.filter`).
  * Always contains **all arguments**, can’t capture partially.
* ⚠️ Arrow functions do not have `arguments`. They inherit from their outer scope.

<br>

### 📌 Spread Syntax

* Opposite of rest → expands an iterable into arguments.
* Example:

  ```js
  let arr = [3, 5, 1];
  console.log(Math.max(...arr)); // 5
  ```
* Can combine multiple iterables:

  ```js
  let arr1 = [1, 2], arr2 = [3, 4];
  console.log([...arr1, ...arr2]); // [1, 2, 3, 4]
  ```
* Works with strings:

  ```js
  console.log([..."Hello"]); // ['H','e','l','l','o']
  ```

<br>

### 📌 Spread vs `Array.from`

* `Array.from(str)` → works with **iterables and array-like**.
* `[...str]` → works only with **iterables**.
* Example:

  ```js
  Array.from("Hi"); // ['H','i']
  [..."Hi"];        // ['H','i']
  ```

<br>

### 📌 Copying Arrays & Objects

* Copy an array:

  ```js
  let arr = [1, 2, 3];
  let arrCopy = [...arr];
  ```
* Copy an object:

  ```js
  let obj = {a:1, b:2};
  let objCopy = {...obj};
  ```

<br>

### 📌 Summary

* **`...` Rest** → gathers remaining arguments into an array (in function definitions).
* **`...` Spread** → expands arrays/iterables into a list (in function calls or array/object literals).
* Use rest to handle **variable arguments**.
* Use spread to **pass arrays, merge arrays/objects, or copy them**.
