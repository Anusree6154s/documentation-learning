

# 📌 `var` in JavaScript (Old Style)

### 🔹 Key Facts

* `var` is **older** than `let`/`const`.
* Rarely used today → mostly seen in **old scripts**.
* Works differently inside functions & blocks.

<br>

## 📌 Differences Between `var` and `let/const`

### 1. ❌ No Block Scope

* `var` ignores `{}` blocks → only **function-scoped** or **global-scoped**.

```js
if (true) {
  var test = "Hi";
}
console.log(test); // "Hi" (still accessible outside block)
```

➡️ With `let`, it would throw error outside block.

<br>

### 2. ✅ Function Scope

```js
function sayHi() {
  if (true) {
    var phrase = "Hello";
  }
  console.log(phrase); // works
}
sayHi();
console.log(phrase); // ❌ ReferenceError
```

<br>

### 3. 🔁 Redeclaration Allowed

* `let/const` → error if redeclared in same scope.
* `var` → silently allows redeclaration.

```js
var user = "Pete";
var user = "John"; // no error
console.log(user); // John
```

<br>

### 4. 📌 Hoisting (Declarations moved up)

* `var` is **hoisted** (declared at top of function/script).
* Only **declaration** is hoisted, not the assignment.

```js
function sayHi() {
  console.log(phrase); // undefined
  var phrase = "Hello";
}
sayHi();
```

Works like:

```js
function sayHi() {
  var phrase;       // hoisted
  console.log(phrase); // undefined
  phrase = "Hello"; // assignment happens here
}
```

<br>

### 5. 🌀 IIFE (Immediately Invoked Function Expression)

* Before `let`, developers used IIFE to create **block-like scope** with `var`.

```js
(function() {
  var msg = "Hello";
  console.log(msg); // Hello
})();  // runs immediately
```

* Different syntax tricks for IIFE:

```js
(function(){})();
(function(){}());
!function(){}();
+function(){}();
```

<br>

## 📌 Summary

* `var` = **function-scoped**, not block-scoped.
* Declarations are **hoisted** to top.
* Allows redeclaration.
* Often wrapped in **IIFEs** in old code.
* Replaced by **`let` & `const`** in modern JavaScript.
