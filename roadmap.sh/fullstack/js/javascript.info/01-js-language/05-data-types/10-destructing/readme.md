

# 📌 Destructuring Assignment (Quick Notes)

### 🔹 What it is

* Special syntax to **unpack arrays/objects** into variables.
* Makes code shorter & clearer.
* Does **not** modify the original array/object.

<br>

## 📌 Array Destructuring

* Basic example:

  ```js
  let [first, last] = ["John", "Smith"];
  ```
* Works with strings, Sets, iterables:

  ```js
  let [a,b,c] = "abc";
  let [x,y] = new Set([1,2]);
  ```
* Skip elements:

  ```js
  let [first, , third] = ["A","B","C"];
  ```
* Assign to object properties:

  ```js
  let user = {};
  [user.name, user.age] = ["Alice", 25];
  ```
* Swap variables:

  ```js
  [a, b] = [b, a];
  ```
* Rest operator:

  ```js
  let [head, ...tail] = [1,2,3,4];
  // head=1, tail=[2,3,4]
  ```
* Default values:

  ```js
  let [name="Guest"] = [];
  ```

<br>

## 📌 Object Destructuring

* Basic usage:

  ```js
  let {title, width, height} = {title:"Menu", width:100, height:200};
  ```
* Order doesn’t matter.
* Rename variables:

  ```js
  let {width: w, height: h} = {width:100, height:200};
  ```
* Defaults:

  ```js
  let {title="Untitled", width=200} = {};
  ```
* Rest:

  ```js
  let {title, ...rest} = {title:"Menu", width:100, height:200};
  ```
* Wrap in parentheses if no `let`:

  ```js
  ({title, width} = {title:"Menu", width:100});
  ```

<br>

## 📌 Nested Destructuring

```js
let options = {
  size: { width: 100, height: 200 },
  items: ["Cake", "Donut"]
};

let {
  size: { width, height },
  items: [item1, item2],
  title="Menu"
} = options;
// width=100, height=200, item1="Cake", title="Menu"
```

<br>

## 📌 Function Parameters with Destructuring

* Instead of many ordered params:

  ```js
  function showMenu({title="Menu", width=100, height=200}={}) {
    console.log(title, width, height);
  }
  showMenu(); // Menu 100 200
  ```
* Supports renaming & nested structures:

  ```js
  function showMenu({title, items:[first,second]}) {
    console.log(first, second);
  }
  ```

<br>

# 📌 Tasks & Solutions

### ✅ Task 1: Destructuring assignment

```js
let user = { name: "John", years: 30 };

// Solution:
let { name, years: age, isAdmin = false } = user;

alert(name);   // John
alert(age);    // 30
alert(isAdmin); // false
```

<br>

### ✅ Task 2: Top Salary

```js
let salaries = {
  "John": 100,
  "Pete": 300,
  "Mary": 250
};

function topSalary(salaries) {
  let maxSalary = 0;
  let maxName = null;

  for (let [name, salary] of Object.entries(salaries)) {
    if (salary > maxSalary) {
      maxSalary = salary;
      maxName = name;
    }
  }
  return maxName;
}

alert(topSalary(salaries)); // Pete
```