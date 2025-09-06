

### 🔹 JavaScript & Host Environments

* JavaScript was created for **browsers**, now used in many platforms (Node.js, servers, even devices).
* Each platform provides its own **host environment** = core JS + extra objects/functions.

<br>

### 🔹 Browser Environment Overview

* Root object = **`window`**:

  1. Acts as the **global object** (all global variables/functions live here).
  2. Represents the **browser window** (has properties like `innerHeight`).

  ```js
  function sayHi() { alert("Hello"); }
  window.sayHi(); // works
  alert(window.innerHeight); // browser window height
  ```

<br>

### 🔹 DOM (Document Object Model)

* Represents **page content as objects**.
* Entry point: **`document`** object.
* Example:

  ```js
  document.body.style.background = "red";
  setTimeout(() => document.body.style.background = "", 1000);
  ```
* Defined in **DOM Living Standard**.
* Used outside browsers too (e.g., server-side HTML parsing).

<br>

### 🔹 CSSOM (CSS Object Model)

* Defines how **CSS rules and stylesheets** are represented as objects.
* Rarely modified directly (usually add/remove classes).
* Still possible to **read/write CSS rules** via JavaScript.

<br>

### 🔹 BOM (Browser Object Model)

* Extra browser objects for **everything beyond the document**.
* Examples:

  * `navigator` → browser & OS info (`userAgent`, `platform`).
  * `location` → current URL, redirects.

    ```js
    alert(location.href);
    location.href = "https://wikipedia.org";
    ```
  * `alert`, `prompt`, `confirm` → browser UI dialogs.
* BOM is defined in the **HTML spec**.

<br>

### 🔹 Specifications

1. **DOM Spec** → Document structure, manipulation, events.
   👉 [https://dom.spec.whatwg.org](https://dom.spec.whatwg.org)
2. **CSSOM Spec** → CSS rules, stylesheets, manipulation.
   👉 [https://www.w3.org/TR/cssom-1/](https://www.w3.org/TR/cssom-1/)
3. **HTML Spec** → HTML language + BOM (browser functions like `setTimeout`, `alert`, `location`).
   👉 [https://html.spec.whatwg.org](https://html.spec.whatwg.org)

   * Extends DOM with extra properties & methods.
4. **Other Specs** → [https://spec.whatwg.org](https://spec.whatwg.org).

<br>

### 🔹 Resources

* **MDN (Mozilla Developer Network)** → Easier to read, great for quick lookup.
  👉 [https://developer.mozilla.org/en-US/](https://developer.mozilla.org/en-US/)
* **WHATWG Specs** → Longer & complex, but authoritative.
* Search tip: `"WHATWG [term]"` or `"MDN [term]"`.

<br>

✅ **Summary**

* **DOM** → document content.
* **CSSOM** → CSS rules.
* **BOM** → browser features (navigator, location, alert, timers).
* **HTML spec** ties everything together.
