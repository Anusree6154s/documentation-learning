
### 🌐 Same Origin Policy

* Protects users from malicious scripts accessing sensitive data across sites.
* **Same origin** → URLs must have the **same protocol, domain, and port**.

**Examples:**

* Same origin:

  ```
  http://site.com
  http://site.com/
  http://site.com/page.html
  ```
* Different origin:

  ```
  http://www.site.com   (different domain)
  https://site.com      (different protocol)
  http://site.com:8080  (different port)
  ```

**Policy:**

* Same origin → full access to window/document.
* Different origin → restricted: **can only write to location**, cannot read content or location.

<br>

### 🖼 Iframes

* Access iframe contents:

  ```js
  iframe.contentWindow   // window object inside iframe
  iframe.contentDocument // document inside iframe
  ```

* **Same origin** → full access.

* **Different origin** → accessing document or reading location throws a SecurityError; can only write to location.

* `iframe.onload` triggers when the iframe’s document fully loads.

**Pitfalls:**

* Immediately after creation, iframe has an **initial document**, which is replaced after load. Avoid interacting with it too early.

**Window collections:**

* `window.frames` → collection of all child windows/iframes.
* `window.parent` → reference to parent window.
* `window.top` → reference to topmost window.

<br>

### 🏷 Subdomains: `document.domain`

* Pages like `a.site.com` and `b.site.com` can interact if both set:

  ```js
  document.domain = 'site.com';
  ```
* **Deprecated** → still supported, but cross-window messaging (`postMessage`) is preferred.

<br>

### 🛡 Iframe sandbox

* Attribute `<iframe sandbox>` enforces restrictions:

  * Defaults → strictest limitations.
  * Can lift certain restrictions via space-separated values:

    ```
    allow-same-origin allow-forms allow-scripts allow-popups allow-top-navigation
    ```
* Purpose → run untrusted code safely.

<br>

### 💬 Cross-window messaging: `postMessage`

* Allows communication **regardless of origin**.

* **Sender:**

  ```js
  targetWindow.postMessage(data, targetOrigin);
  ```

  * `data` → message (any object; IE supports only strings).
  * `targetOrigin` → restricts which window can receive the message.

* **Receiver:**

  ```js
  window.addEventListener("message", function(event) {
    if(event.origin !== 'http://trusted.com') return; // security check
    console.log(event.data);        // message
    event.source.postMessage(...);  // optional reply
  });
  ```

<br>

### ✅ Summary

* References to other windows:

  * `window.open()` → returns reference to new window.
  * `window.opener` → reference from popup to opener.
  * `iframe.contentWindow` → window inside iframe.
  * `window.frames`, `window.parent`, `window.top` → iframe hierarchy.

* **Same origin:** full access.

* **Different origin:** restricted access → can only:

  1. Change location.
  2. Use `postMessage` to communicate.

* Exceptions:

  * Pages with same second-level domain + `document.domain`.
  * Sandbox iframe without `allow-same-origin`.

* `postMessage` → safe way for cross-origin communication, with `origin` check for security.
