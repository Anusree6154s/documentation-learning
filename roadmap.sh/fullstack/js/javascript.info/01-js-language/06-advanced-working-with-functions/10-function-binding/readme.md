

# 📌 Function Binding in JavaScript

## 🔹 Problem: Losing `this`

* Passing object methods (e.g., to `setTimeout`) often **loses `this`**.
* Example:

  ```js
  let user = { firstName: "John", sayHi() { alert(this.firstName); } };
  setTimeout(user.sayHi, 1000); // ❌ undefined
  ```

  Because method is **detached from object** → `this` becomes `window` (browser) / `undefined` (strict mode).

<br>

## 🔹 Solution 1: Wrapper Function

* Wrap call in function:

  ```js
  setTimeout(() => user.sayHi(), 1000);
  ```
* ✅ Works, but ❌ fails if `user` changes before timeout.

<br>

## 🔹 Solution 2: `bind`

* `func.bind(context)` → returns new function with fixed `this`.
* Example:

  ```js
  let sayHi = user.sayHi.bind(user);
  setTimeout(sayHi, 1000); // ✅ works
  ```
* Arguments still pass normally.

<br>

## 🔹 Partial Functions with `bind`

* Can fix arguments too:

  ```js
  function mul(a, b) { return a * b; }
  let double = mul.bind(null, 2);
  double(3); // 6
  ```
* Useful for making specific variants (`double`, `triple`).

<br>

## 🔹 Custom `partial` (without fixing `this`)

```js
function partial(func, ...argsBound) {
  return function(...args) {
    return func.call(this, ...argsBound, ...args);
  };
}
```

* Keeps `this`, fixes some args only.

<br>

## 📌 Summary

* `bind` fixes `this` (and optionally some args).
* Used to prevent **losing `this`** when passing methods as callbacks.
* Partial application = fixing some arguments for convenience.

<br>

# 📝 Tasks & Solutions

### 1. Bound function as a method

```js
function f() { alert(this); }
let user = { g: f.bind(null) };
user.g(); 
// ❌ null (because bind fixed this=null, not user)
```

<br>

### 2. Second bind

```js
function f() { alert(this.name); }
f = f.bind({name: "John"}).bind({name: "Ann"});
f(); 
// John ✅ (first bind wins, later binds ignored)
```

<br>

### 3. Function property after bind

```js
function sayHi() {}
sayHi.test = 5;
let bound = sayHi.bind({name: "John"});
alert(bound.test); // undefined ❌
// Because bind returns a new function (no .test property)
```

<br>

### 4. Fix function losing `this`

```js
askPassword(user.loginOk.bind(user), user.loginFail.bind(user));
```

<br>

### 5. Partial application for login

```js
askPassword(user.login.bind(user, true), user.login.bind(user, false));
```