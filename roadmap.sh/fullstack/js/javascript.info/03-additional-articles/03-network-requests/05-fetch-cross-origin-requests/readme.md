
### 1. Core Concept

* **Origin** = triplet: domain + protocol + port.
* **Cross-Origin Request** = when origin differs in any part.
* **CORS (Cross-Origin Resource Sharing)** = security policy requiring server to explicitly allow cross-origin access.

<br>

### 2. History (Why CORS Exists)

* Old rule: scripts from one site cannot access another site’s content → protected users.
* Workarounds before CORS:

  * `<form>` submission into `<iframe>` (could send data but not read response).
  * `<script src="...">` (JSONP) → executed cross-domain script that called local callback.

<br>

### 3. Safe vs Unsafe Requests

**Safe Requests** (sent directly, no preflight):

* Methods: `GET`, `POST`, `HEAD`.
* Headers: only `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` (with `application/x-www-form-urlencoded`, `multipart/form-data`, or `text/plain`).

**Unsafe Requests** (require preflight):

* Any other method (e.g. `PUT`, `DELETE`, `PATCH`).
* Custom headers (e.g. `API-Key`).
* Non-standard `Content-Type`.

<br>

### 4. Safe Requests Flow

* Browser sends request with **Origin** header.
* Server must respond with:

  * `Access-Control-Allow-Origin: <origin>` or `*`.
  * Optionally `Access-Control-Expose-Headers` → allows JS to read non-safe headers.
* Browser enforces access: if headers don’t match → error.

<br>

### 5. Unsafe Requests Flow (Preflight)

1. **Preflight request (OPTIONS)** sent by browser automatically.

   * Headers:

     * `Origin`
     * `Access-Control-Request-Method`
     * `Access-Control-Request-Headers`
2. **Server response** must include:

   * `Access-Control-Allow-Origin`
   * `Access-Control-Allow-Methods`
   * `Access-Control-Allow-Headers`
   * Optional: `Access-Control-Max-Age` (cache time for preflight).
3. If approved → main request is sent, again with `Origin` header.
4. Main response must also include `Access-Control-Allow-Origin`.

<br>

### 6. Credentials

* By default, **no cookies/HTTP-auth** sent in cross-origin fetch.
* To include → `fetch(url, { credentials: "include" })`.
* Server must respond with:

  * `Access-Control-Allow-Origin: <exact-origin>` (not `*`).
  * `Access-Control-Allow-Credentials: true`.

<br>

### 7. Origin vs Referer

* `Referer` → full URL of the request source (can expose too much info).
* `Origin` → only scheme + domain + port (minimal, privacy-friendly).
* Sometimes `Referer` may be missing or stripped (privacy, redirects, HTTPS→HTTP), but `Origin` is reliable for CORS security.

<br>

### 8. Summary

* **Safe requests**: direct, only limited methods/headers.
* **Unsafe requests**: preflight → server must explicitly allow.
* **Headers to know**:

  * Request: `Origin`, `Access-Control-Request-Method`, `Access-Control-Request-Headers`.
  * Response: `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`, `Access-Control-Expose-Headers`, `Access-Control-Allow-Credentials`, `Access-Control-Max-Age`.
* **Credentials** require explicit opt-in by both client and server.
