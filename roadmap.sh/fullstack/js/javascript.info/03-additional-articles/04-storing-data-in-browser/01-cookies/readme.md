

## 🔹 What Are Cookies?

* Small strings of data stored in the browser.
* Part of the **HTTP protocol (RFC 6265)**.
* Set by server via `Set-Cookie` response header.
* Browser automatically sends cookies back with requests via `Cookie` header.
* Common use case → authentication (session ID).
* Can also be accessed/modified with `document.cookie` in JavaScript.

<br>

## 🔹 Reading Cookies

* `document.cookie` → returns all cookies as `name=value; name2=value2; ...`
* To find a cookie → split by `;` or use regex/array helpers.

<br>

## 🔹 Writing Cookies

* `document.cookie = "user=John";` → sets/updates one cookie (does not overwrite others).
* Must **encode** names/values with `encodeURIComponent()`.
* Limitations:

  * Can set/update only **one cookie at a time**.
  * Each cookie ≤ **4KB**.
  * Per-domain cookies: \~20+ (browser-dependent).

<br>

## 🔹 Cookie Attributes

* Added after `name=value`, separated by `;`.
* Example:

  ```js
  document.cookie = "user=John; path=/; expires=Tue, 19 Jan 2038 03:14:07 GMT";
  ```

### 1. **domain**

* By default → cookie available only on the domain that set it.
* Not shared with subdomains unless explicitly set:

  ```js
  document.cookie = "user=John; domain=site.com";
  ```
* Legacy `.site.com` with dot is now ignored.

### 2. **path**

* Restricts cookie to a URL path.
* Example: `path=/admin` → valid for `/admin` and subpaths, not for `/home`.
* Usually set to `path=/` for site-wide access.

### 3. **expires / max-age**

* By default → cookie deleted when browser closes (session cookie).
* `expires` → date/time in GMT.
* `max-age` → number of seconds (preferred).

  ```js
  document.cookie = "user=John; max-age=3600"; // expires in 1 hour
  document.cookie = "user=John; max-age=0";   // deletes cookie
  ```

### 4. **secure**

* Only sent over **HTTPS**.

  ```js
  document.cookie = "user=John; secure";
  ```

### 5. **samesite**

* Protects from **XSRF attacks**.
* Values:

  * `strict` → never sent on cross-site requests (most secure, but may break UX).
  * `lax` (default in many browsers) → allows cookies on **safe GET + top-level navigation**.
* Helps prevent cross-site form submissions from sending cookies.

### 6. **httpOnly**

* Set by server, not accessible via JavaScript.
* Protects against XSS stealing cookies.

<br>

## 🔹 Special Topics

### ❖ XSRF (Cross-Site Request Forgery)

* Attack where malicious site submits a form to victim’s bank with user’s cookies.
* `samesite` mitigates this risk.

### ❖ Third-Party Cookies

* Set by domains other than the current page (e.g., ads, trackers).
* Blocked by Safari by default, restricted in Firefox/Chrome.
* If a third-party script sets a cookie → it belongs to the **current page’s domain**, not the script’s origin.

### ❖ GDPR

* In EU → need explicit user consent for **tracking/identifying cookies**.
* Websites often use modals or checkboxes for compliance.

<br>

## 🔹 Helper Functions

* `getCookie(name)` → retrieves cookie by name.
* `setCookie(name, value, attributes)` → convenient setter.
* `deleteCookie(name)` → deletes by setting `max-age=-1`.

<br>

## 🔹 Summary

* `document.cookie` → read/write cookies.
* Restrictions: single cookie at a time, ≤4KB each, \~20 per domain.
* Key attributes:

  * `path`, `domain` → scope.
  * `expires`, `max-age` → lifetime.
  * `secure`, `samesite`, `httpOnly` → security.
* Third-party & tracking cookies → subject to browser rules + GDPR.
