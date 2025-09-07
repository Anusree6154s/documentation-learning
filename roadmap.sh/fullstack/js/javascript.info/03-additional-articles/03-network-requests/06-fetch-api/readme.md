
## 🔹 Full Fetch Options (with defaults)

```js
fetch(url, {
  method: "GET",              // POST, PUT, DELETE, etc.
  headers: { "Content-Type": "text/plain;charset=UTF-8" },
  body: undefined,            // string, FormData, Blob, BufferSource, URLSearchParams
  referrer: "about:client",   // or "" (no Referer), or same-origin URL
  referrerPolicy: "strict-origin-when-cross-origin", 
  mode: "cors",               // same-origin, no-cors
  credentials: "same-origin", // omit, include
  cache: "default",           // no-store, reload, no-cache, force-cache, only-if-cached
  redirect: "follow",         // manual, error
  integrity: "",              // checksum like "sha256-abcdef"
  keepalive: false,           // allow request after page unload
  signal: undefined,          // AbortController
  window: window              // null
});
```

<br>

## 🔹 `referrer` and `referrerPolicy`

* **`referrer`**: manually set or remove `Referer` header.

  * `""` → no referrer.
  * `"https://site.com/page"` → custom referrer (same origin only).

* **`referrerPolicy`**: rules for how much of referrer to send.

  | Value                                       | Same Origin | Cross Origin | HTTPS → HTTP |
  | ------------------------------------------- | ----------- | ------------ | ------------ |
  | `no-referrer`                               | –           | –            | –            |
  | `no-referrer-when-downgrade`                | full        | full         | –            |
  | `origin`                                    | origin      | origin       | origin       |
  | `origin-when-cross-origin`                  | full        | origin       | origin       |
  | `same-origin`                               | full        | –            | –            |
  | `strict-origin`                             | origin      | origin       | –            |
  | `strict-origin-when-cross-origin` (default) | full        | origin       | –            |
  | `unsafe-url`                                | full        | full         | full         |

<br>

## 🔹 `mode`

* Controls **cross-origin** behavior:

  * `"cors"` (default) → allow cross-origin (with CORS headers).
  * `"same-origin"` → block cross-origin.
  * `"no-cors"` → only “safe” cross-origin requests allowed.

<br>

## 🔹 `credentials`

* Controls **cookies & auth headers**:

  * `"same-origin"` (default) → send only for same-origin.
  * `"include"` → always send (needs `Access-Control-Allow-Credentials`).
  * `"omit"` → never send.

<br>

## 🔹 `cache`

* Controls **HTTP cache usage**:

  * `"default"` → standard cache rules.
  * `"no-store"` → ignore cache completely.
  * `"reload"` → bypass cache but update it.
  * `"no-cache"` → conditional request if cached, else fresh fetch.
  * `"force-cache"` → use cached response even if stale.
  * `"only-if-cached"` → use cached response or fail (only `same-origin`).

<br>

## 🔹 `redirect`

* Handle HTTP redirects (301, 302, …):

  * `"follow"` (default) → follow automatically.
  * `"error"` → throw error on redirect.
  * `"manual"` → return special `opaqueredirect` response (handle manually).

<br>

## 🔹 `integrity`

* Verifies response against checksum (`Subresource Integrity`).
* Example:

  ```js
  fetch("file.js", { integrity: "sha256-abcdef123..." });
  ```
* If mismatch → request fails.

<br>

## 🔹 `keepalive`

* Allows request to **outlive the page** (important for analytics).
* Example:

  ```js
  window.onunload = () => {
    fetch("/analytics", {
      method: "POST",
      body: "stats",
      keepalive: true
    });
  };
  ```
* Limitations:

  * Max **64KB total body** (per page).
  * No response handling after unload.

<br>

## 🔹 Summary

* `referrer` / `referrerPolicy` → control **Referer** header.
* `mode` → limit cross-origin.
* `credentials` → manage cookies/auth.
* `cache` → fine-grain caching.
* `redirect` → follow, block, or manual handling.
* `integrity` → checksum validation.
* `keepalive` → send requests after unload (analytics use).
