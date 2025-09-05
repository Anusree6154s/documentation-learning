

## 🔹 Static imports (limitations)

* Must use a **string literal** as the module path.

  ```js
  import ... from getModuleName(); // ❌ Error
  ```
* Cannot be used **conditionally** or inside blocks.

  ```js
  if (true) { import ... } // ❌ Error
  ```
* Reason: static imports allow:

  * **Code structure analysis**
  * **Bundling into one file**
  * **Tree-shaking** (removing unused exports)

<br>

## 🔹 Dynamic import syntax

* `import(modulePath)` → returns a **Promise** resolving to the module object.
* Can be used **anywhere in code**.
* Works in **regular scripts** (no need for `type="module"`).

```js
let modulePath = './say.js';
import(modulePath)
  .then(module => { /* use exports */ })
  .catch(err => console.error(err));
```

* With `await` inside async functions:

  ```js
  let module = await import('./say.js');
  ```

<br>

## 🔹 Example with named exports

```js
// say.js
export function hi() { alert("Hello"); }
export function bye() { alert("Bye"); }

let { hi, bye } = await import('./say.js');
hi(); // Hello
bye(); // Bye
```

<br>

## 🔹 Example with default export

```js
// say.js
export default function() {
  alert("Module loaded (default)!");
}

let obj = await import('./say.js');
let say = obj.default;
// or shorter:
let { default: say } = await import('./say.js');

say(); // "Module loaded (default)!"
```

<br>

## 🔹 Full example in HTML

```html
<!doctype html>
<script>
  async function load() {
    let say = await import('./say.js');
    say.hi();
    say.bye();
    say.default();
  }
</script>
<button onclick="load()">Click me</button>
```

<br>

## 🔹 Key notes

* `import()`:

  * Looks like a function but is **special syntax** (like `super()`).
  * Cannot be assigned to a variable or called with `.apply()`/`.call()`.
* Useful for:

  * On-demand loading.
  * Conditional loading.
  * Performance optimization.
