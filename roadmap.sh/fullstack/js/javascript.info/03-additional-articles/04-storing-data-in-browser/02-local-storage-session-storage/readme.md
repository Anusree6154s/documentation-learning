
## 🔹 Why use Web Storage?

* Alternative to **cookies**, but:

  * Not sent to the server with every request.
  * Much larger capacity (5MB+).
  * JavaScript-only (server cannot modify).
* Bound to **origin** (protocol + domain + port).

<br>

## 🔹 Common API (for both)

* `setItem(key, value)` → store string.
* `getItem(key)` → retrieve value.
* `removeItem(key)` → delete key.
* `clear()` → delete all.
* `key(index)` → get key at index.
* `length` → number of stored keys.

⚠️ Both key and value are **strings**.

* To store objects → use `JSON.stringify()` / `JSON.parse()`.

<br>

## 🔹 localStorage

* Shared across all tabs/windows of the same origin.
* Survives **browser restart**.
* Example:

  ```js
  localStorage.setItem("theme", "dark");
  console.log(localStorage.getItem("theme")); // dark
  ```

<br>

## 🔹 sessionStorage

* Scoped to **one browser tab** (but shared with same-origin iframes inside it).
* Survives **page refresh**, but not tab close.
* Example:

  ```js
  sessionStorage.setItem("user", "Alice");
  console.log(sessionStorage.getItem("user")); // Alice
  ```

<br>

## 🔹 Object-like access

```js
localStorage.test = 123;
console.log(localStorage.test); // 123
delete localStorage.test;
```

⚠️ Not recommended → can conflict with built-in keys (`length`, `toString`) & doesn’t trigger `storage` event.

<br>

## 🔹 Iterating Keys

* Using `key(index)`:

  ```js
  for (let i = 0; i < localStorage.length; i++) {
    let key = localStorage.key(i);
    console.log(key, localStorage.getItem(key));
  }
  ```
* Or safer:

  ```js
  Object.keys(localStorage).forEach(key => {
    console.log(key, localStorage.getItem(key));
  });
  ```

<br>

## 🔹 storage Event

* Fires on **other windows/tabs**, not the one that made the change.
* Properties:

  * `key` → changed key.
  * `oldValue`, `newValue`.
  * `url` → source document URL.
  * `storageArea` → `localStorage` or `sessionStorage`.
* Example:

  ```js
  window.onstorage = e => {
    console.log(`${e.key} changed from ${e.oldValue} to ${e.newValue} in ${e.url}`);
  };
  ```

<br>

## 🔹 Use Case: Autosave Form

```html
<textarea id="message"></textarea>

<script>
let textarea = document.getElementById("message");

// Load saved value on page load
if (localStorage.getItem("autosave")) {
  textarea.value = localStorage.getItem("autosave");
}

// Save on every input
textarea.addEventListener("input", () => {
  localStorage.setItem("autosave", textarea.value);
});
</script>
```

✅ If the user refreshes or reopens, unfinished text stays.

<br>

## 🔹 Summary: localStorage vs sessionStorage

| Feature  | localStorage                                      | sessionStorage                               |
| -------- | ------------------------------------------------- | -------------------------------------------- |
| Scope    | All tabs/windows of same origin                   | Single tab (shared with same-origin iframes) |
| Lifetime | Until explicitly cleared (persists after restart) | Until tab is closed (persists on refresh)    |
| Size     | 5MB+                                              | 5MB+                                         |
| API      | Same                                              | Same                                         |
