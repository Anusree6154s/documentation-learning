

# 🌐 Fetch API (Quick Notes)

## 1. Basics

* `fetch(url, [options])` → returns a **Promise**.
* Default: `GET` request.
* Promise resolves with **Response object** (status + headers, not body yet).
* Promise rejects only on **network failure** (not on 404/500).

<br>

## 2. Response Object

* `response.status` → HTTP status code.
* `response.ok` → `true` if `200–299`.
* `response.headers` → Map-like, can `.get()` or iterate.

<br>

## 3. Reading Response Body

Only **one body method allowed** per response.

* `response.text()` → returns body as string.
* `response.json()` → parses JSON.
* `response.formData()` → body as FormData.
* `response.blob()` → body as Blob (binary + type).
* `response.arrayBuffer()` → low-level binary data.
* `response.body` → `ReadableStream` (manual chunk reading).

<br>

## 4. Request Headers

* Set with `headers` option:

  ```js
  fetch(url, { headers: { 'Content-Type': 'application/json' } })
  ```
* ❌ Forbidden headers (browser-controlled): `Content-Length`, `Cookie`, `Origin`, `Host`, etc.

<br>

## 5. POST Requests

* Options:

  * `method`: e.g. `"POST"`.
  * `body`: data (`string`, `FormData`, `Blob`, `URLSearchParams`).
* Default `Content-Type`: `text/plain;charset=UTF-8`.
* For JSON → must set manually:

  ```js
  headers: { 'Content-Type': 'application/json' }
  body: JSON.stringify(data)
  ```

<br>

## 6. Binary Data (Blob)

* Example: sending `<canvas>` image.
* `canvas.toBlob(resolve, 'image/png')` → generates blob.
* Fetch sends it with `body: blob`.
* Browser auto-sets correct `Content-Type` for blob.

<br>

## 7. Summary Workflow

```js
let response = await fetch(url, options); // headers only
let result = await response.json(); // body
```

Or with `.then()` chaining.

<br>

# 📝 Task: Fetch Users from GitHub

## Requirement

* Function `getUsers(names)` → array of GitHub users.
* URL: `https://api.github.com/users/USERNAME`.
* Rules:

  * One fetch per user.
  * Don’t wait sequentially → run in parallel.
  * If fetch fails or user not found → `null`.

<br>

## Solution

```js
async function getUsers(names) {
  let requests = names.map(name =>
    fetch(`https://api.github.com/users/${name}`)
      .then(response => response.ok ? response.json() : null)
      .catch(() => null)
  );
  
  return Promise.all(requests);
}
```
 