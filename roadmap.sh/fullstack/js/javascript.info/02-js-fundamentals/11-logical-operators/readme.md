

# 📌 Logical Operators in JavaScript

### 1. `||` (OR)

* **Boolean meaning**: `true` if *any* operand is truthy.
* **JS extension**: returns **first truthy value**, or last value if all falsy.
* **Short-circuits** → stops at first truthy.

Example:

```js
alert( 1 || 0 );         // 1
alert( null || "hi" );   // "hi"
alert( undefined || 0 ); // 0 (last, all falsy)
```

<br>

### 2. `&&` (AND)

* **Boolean meaning**: `true` only if *all* operands are truthy.
* **JS extension**: returns **first falsy value**, or last value if all truthy.
* **Short-circuits** → stops at first falsy.

Example:

```js
alert( 1 && 0 );        // 0
alert( 1 && 5 );        // 5
alert( 1 && 2 && 3 );   // 3 (all truthy, return last)
```

<br>

### 3. `!` (NOT)

* Converts value → boolean, then negates it.
* Double NOT (`!!`) converts any value to boolean.

Example:

```js
alert( !true );          // false
alert( !!"non-empty" );  // true
alert( !!0 );            // false
```
