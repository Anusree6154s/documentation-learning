

## 🔹 Async Functions

1. `async` before a function:

   * Ensures the function **always returns a Promise**.
   * Non-promises are wrapped into a resolved Promise.

   ```js
   async function f() { return 1; }
   f().then(alert); // 1
   ```

<br>

## 🔹 Await

2. Syntax:

   ```js
   let result = await promise;
   ```

   * Waits until the promise settles.
   * Returns the resolved value OR throws the error.

3. Works **only inside async functions** (or top-level in modules).

   ```js
   function f() {
     let result = await Promise.resolve(1); // ❌ Error
   }
   ```

4. Execution is paused without blocking CPU → JS engine can handle other tasks.

<br>

## 🔹 Examples

5. Simple usage:

   ```js
   async function f() {
     let promise = new Promise(resolve => setTimeout(() => resolve("done!"), 1000));
     let result = await promise;  
     alert(result); // "done!"
   }
   ```

6. Async class methods:

   ```js
   class Waiter {
     async wait() {
       return await Promise.resolve(1);
     }
   }
   new Waiter().wait().then(alert); // 1
   ```

<br>

## 🔹 Thenables

7. Await works on **thenable objects** (any object with `.then` method).

   ```js
   class Thenable {
     constructor(num) { this.num = num; }
     then(resolve) { setTimeout(() => resolve(this.num * 2), 1000); }
   }
   async function f() { alert(await new Thenable(1)); } // 2
   ```

<br>

## 🔹 Error Handling

8. Await throws on rejection:

   ```js
   async function f() {
     try {
       let response = await fetch("bad-url");
     } catch (err) {
       alert(err);
     }
   }
   ```

9. If not caught → function returns a rejected Promise:

   ```js
   async function f() {
     await Promise.reject(new Error("Whoops!"));
   }
   f().catch(alert);
   ```

<br>

## 🔹 Top-level Await

10. Modern browsers allow **top-level await** in ES modules:

    ```js
    let response = await fetch('/data.json');
    let user = await response.json();
    ```

11. If not in module → wrap in async IIFE:

    ```js
    (async () => {
      let response = await fetch('/data.json');
      console.log(await response.json());
    })();
    ```

<br>

## 🔹 Async vs .then

12. Async/await replaces most `.then` chains.

    * Use `try..catch` instead of `.catch`.
    * Still need `.then/.catch` for **top-level handling**.

<br>

## 🔹 Promise.all with Async

13. Use with multiple promises:

    ```js
    let results = await Promise.all([
      fetch(url1),
      fetch(url2),
    ]);
    ```

    * If **any fails** → error propagates.

<br>

## 🔹 Tasks

14. **Rewrite using async/await**

```js
async function loadJson(url) {
  let response = await fetch(url);
  if (response.status == 200) {
    return await response.json();
  } else {
    throw new Error(response.status);
  }
}

loadJson('https://javascript.info/no-such-user.json')
  .catch(alert); // Error: 404
```

15. **Rewrite “rethrow” with async/await**

```js
class HttpError extends Error {
  constructor(response) {
    super(`${response.status} for ${response.url}`);
    this.response = response;
  }
}

async function loadJson(url) {
  let response = await fetch(url);
  if (response.status == 200) return response.json();
  throw new HttpError(response);
}

async function demoGithubUser() {
  while (true) {
    let name = prompt("Enter a name?", "iliakan");
    try {
      let user = await loadJson(`https://api.github.com/users/${name}`);
      alert(`Full name: ${user.name}`);
      return user;
    } catch (err) {
      if (err instanceof HttpError && err.response.status == 404) {
        alert("No such user, please reenter.");
      } else throw err;
    }
  }
}

demoGithubUser();
```

16. **Call async from non-async**

```js
async function wait() {
  await new Promise(resolve => setTimeout(resolve, 1000));
  return 10;
}

function f() {
  wait().then(result => alert(result)); // 10
}
```

17. **Dangerous Promise.all**

* Problem: `Promise.all` stops on **first rejection**, but other promises keep running → errors after disconnect.
* Fix: handle errors **inside each query**:

  ```js
  await Promise.all([
    delay(() => database.query(true).catch(err => console.log(err)), 100),
    delay(() => database.query(false).catch(err => console.log(err)), 200),
    delay(() => database.query(false).catch(err => console.log(err)), 300),
  ]);
  ```
* Or use `Promise.allSettled` to wait for all results safely.

<br>

✅ Summary:

* `async` → returns promise, allows `await`.
* `await` → pauses until settled, returns value or throws.
* Use `try..catch` for errors.
* `Promise.all` + async/await = parallel tasks, but beware of rejection behavior.
