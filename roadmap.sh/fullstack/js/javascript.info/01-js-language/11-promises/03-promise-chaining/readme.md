

### 🔗 Promise chaining basics

* Promises allow you to perform asynchronous tasks **one after another** in sequence.
* Each `.then` returns a **new promise** → the next `.then` runs when that promise settles.
* If a handler returns a value → it becomes the result for the next `.then`.
* If a handler returns a promise → the chain waits until it resolves before moving on.

<br>

### ✅ Example: simple chaining

```js
new Promise(resolve => setTimeout(() => resolve(1), 1000))
  .then(result => {
    alert(result); // 1
    return result * 2;
  })
  .then(result => {
    alert(result); // 2
    return result * 2;
  })
  .then(result => {
    alert(result); // 4
  });
```

Flow: `1 → 2 → 4`.

<br>

### ❌ Common mistake

Adding multiple `.then` to the **same promise** is *not* chaining:

```js
promise.then(r => alert(r)); 
promise.then(r => alert(r)); 
```

All handlers get the **same result** → not passed along.

<br>

### 📌 Returning promises

* A `.then` handler can return a **new promise**.
* The next handler waits until it resolves.

```js
new Promise(resolve => setTimeout(() => resolve(1), 1000))
  .then(result => new Promise(res => setTimeout(() => res(result * 2), 1000)))
  .then(result => alert(result)); // 2 after 2 seconds
```

<br>

### 📚 Example: load scripts in sequence

**With chaining (preferred):**

```js
loadScript("one.js")
  .then(() => loadScript("two.js"))
  .then(() => loadScript("three.js"))
  .then(() => {
    one();
    two();
    three();
  });
```

**Without chaining (nested → pyramid of doom):**

```js
loadScript("one.js").then(() => {
  loadScript("two.js").then(() => {
    loadScript("three.js").then(() => {
      one(); two(); three();
    });
  });
});
```

<br>

### ⚡ Thenables

* If an object has a `.then` method, it behaves like a promise.

```js
class Thenable {
  constructor(num) { this.num = num; }
  then(resolve) {
    setTimeout(() => resolve(this.num * 2), 1000);
  }
}
new Promise(res => res(1))
  .then(result => new Thenable(result))
  .then(alert); // 2
```

<br>

### 🌐 Example with `fetch`

```js
fetch('/user.json')
  .then(r => r.json())
  .then(user => fetch(`https://api.github.com/users/${user.name}`))
  .then(r => r.json())
  .then(githubUser => showAvatar(githubUser))
  .then(githubUser => alert(`Finished showing ${githubUser.name}`));
```

Helper functions:

```js
function loadJson(url) {
  return fetch(url).then(r => r.json());
}
function loadGithubUser(name) {
  return loadJson(`https://api.github.com/users/${name}`);
}
function showAvatar(user) {
  return new Promise(resolve => {
    let img = document.createElement("img");
    img.src = user.avatar_url;
    document.body.append(img);
    setTimeout(() => { img.remove(); resolve(user); }, 3000);
  });
}
```

<br>

### 📌 Summary

* `.then` always returns a **new promise**.
* Returning a value → passes value to next `.then`.
* Returning a promise → next `.then` waits for it.
* Use chaining → avoids callback hell ("pyramid of doom").
* Async actions should always **return a promise** → keeps chain extendable.
