

# 📡 XMLHttpRequest (XHR) — Quick Notes

## 1. What it is

* Built-in browser object for HTTP requests.
* Older than `fetch`, still used for:

  * Legacy code support.
  * Old browsers (no polyfills).
  * Features `fetch` lacks (e.g. **upload progress tracking**).
* Supports **async** (default) & **sync** requests (sync = blocking, discouraged).

<br>

## 2. Basic Workflow

1. **Create**: `let xhr = new XMLHttpRequest();`
2. **Initialize**: `xhr.open(method, URL, [async=true, user, pass]);`

   * Does not send yet, just configures.
3. **Send**: `xhr.send([body]);`

   * `GET` → no body.
   * `POST` → send `body` (string, JSON, FormData, Blob).
4. **Listen to events**:

   * `load` → request finished (success or HTTP error).
   * `error` → network failure (not 404/500).
   * `progress` → periodically while downloading.

<br>

## 3. Response Properties

* `xhr.status` → HTTP status (200, 404, …).
* `xhr.statusText` → status message (`OK`, `Not Found`, …).
* `xhr.response` → body (type depends on `responseType`).
* Old props: `xhr.responseText`, `xhr.responseXML` (legacy).

<br>

## 4. Response Types

Set with `xhr.responseType`:

* `""` / `"text"` → string (default).
* `"json"` → auto-parsed JSON.
* `"blob"` → binary Blob.
* `"arraybuffer"` → binary ArrayBuffer.
* `"document"` → XML/HTML document.

<br>

## 5. Ready States

* `0` = UNSENT
* `1` = OPENED
* `2` = HEADERS\_RECEIVED
* `3` = LOADING (receiving data)
* `4` = DONE
* Old handler: `readystatechange` (rarely used now).

<br>

## 6. Timeout

```js
xhr.timeout = 10000; // ms
xhr.ontimeout = () => { ... }
```

<br>

## 7. Aborting

```js
xhr.abort(); // cancels request
```

→ triggers `abort` event, `status = 0`.

<br>

## 8. HTTP Headers

* Set request: `xhr.setRequestHeader(name, value)`.
* ❌ Some headers forbidden (`Referer`, `Host`, `Cookie`, etc.).
* Multiple calls add values → not overwrite.
* Read response:

  * `xhr.getResponseHeader(name)`
  * `xhr.getAllResponseHeaders()` (except `Set-Cookie`).

<br>

## 9. Sending Data

### FormData

```js
let formData = new FormData(form);
formData.append("field", "value");
xhr.send(formData); // multipart/form-data
```

### JSON

```js
xhr.setRequestHeader("Content-Type", "application/json");
xhr.send(JSON.stringify(obj));
```

<br>

## 10. Upload Progress

* Download progress → `xhr.onprogress`.
* Upload progress → `xhr.upload.onprogress`.
* Upload events: `loadstart`, `progress`, `abort`, `error`, `load`, `timeout`, `loadend`.

<br>

## 11. Cross-Origin

* Supports **CORS** (same as `fetch`).
* Cookies/HTTP-auth not sent by default.
* Enable with:

  ```js
  xhr.withCredentials = true;
  ```

<br>

## 12. Lifecycle Events (modern)

* `loadstart` → request begins.
* `progress` → receiving response chunk.
* `abort` → request canceled.
* `error` → network error.
* `load` → finished successfully.
* `timeout` → canceled due to timeout.
* `loadend` → always triggers at end.
