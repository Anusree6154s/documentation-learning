

## **`new Function` Syntax**

* Create a function dynamically from a **string**.
* Syntax:

  ```js
  let func = new Function([arg1, arg2, ...argN], functionBody);
  ```
* Examples:

  ```js
  let sum = new Function('a', 'b', 'return a + b');
  sum(1, 2); // 3

  let sayHi = new Function('alert("Hello")');
  sayHi(); // Hello
  ```

<br>

## **Key Characteristics**

* Function code is provided as a **string**, at runtime.
* Useful when code is not known beforehand (e.g., received from server).
* Alternative to `eval` → safer and scoped only to global env.

<br>

## **Closure Difference**

* Normal functions:

  * Remember their **Lexical Environment** (where they were created).

  ```js
  function getFunc() {
    let value = "test";
    return function() { alert(value); };
  }
  getFunc()(); // "test"
  ```
* `new Function`:

  * Created with **global scope only**, no access to outer variables.

  ```js
  function getFunc() {
    let value = "test";
    return new Function('alert(value)');
  }
  getFunc()(); // Error: value is not defined
  ```

<br>

## **Why This Restriction Exists**

* Prevents problems with:

  * **Minifiers** → local variables renamed (`userName → a`), new Function wouldn’t find them.
  * **Code architecture** → avoids hidden dependencies on outer scopes.
* Forces explicit parameter passing → more reliable.

<br>

## **Argument Variants**

All equivalent:

```js
new Function('a', 'b', 'return a + b');
new Function('a,b', 'return a + b');
new Function('a , b', 'return a + b');
```

<br>

## **Summary**

* `new Function` = create functions from **strings** at runtime.
* Scope = always **global**, no access to local outer variables.
* Safer with minifiers, avoids errors.
* Use **arguments** to pass values in.
* Rarely used, but useful for:

  * Dynamic code execution (templates, server-sent code).
