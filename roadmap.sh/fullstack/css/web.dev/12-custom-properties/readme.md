
##  CSS Custom Properties (Variables)

### 1. **Definition & Syntax**

* Custom properties = user-defined CSS variables.
* Must start with **two dashes `--`**.

  ```css
  .card { --base-size: 1em; }
  ```
* Accessed with **`var(--name)`**.

  ```css
  font-size: calc(2 * var(--base-size));
  ```



### 2. **Where to Define**

* Often initialized on `:root` for global availability.
* Still **overridable** on child elements.

  ```css
  :root { --primary-color: dodgerblue; }
  ```



### 3. <mark>**Fallbacks**</amrk>

* <mark>If a property is undefined, you can give a **fallback** inside `var()`.</mark>

  ```css
  background: var(--alert-bg, var(--default-bg));
  ```



### 4. **Invalid Values**

* If a custom property produces an **invalid value**, the browser discards the declaration.

  * Example: using `1em` for `background-color` is invalid → property falls back to **initial/inherited** value.



### 5. **Inheritance & Overriding**

* Custom properties **inherit by default**.
* They follow normal **cascade rules** (specificity, order, importance).
* Child elements get the parent’s value unless overridden.



### 6. <mark> **`@property` Rule** </mark>

* <mark>Gives **more control** over custom properties.</mark>
* Define syntax, inheritance, and an initial value.

  ```css
  @property --base-size {
    syntax: "<length>";
    inherits: true;
    initial-value: 18px;
  }
  ```
* Benefits:

  * Type checking (invalid values rejected).
  * Control inheritance (`inherits: false`).
  * Guarantees an **initial value**.


### 7. **JavaScript Integration**

* Update variables dynamically with JS:

  ```js
  element.style.setProperty("--color", "orange");
  ```
* Read variable values:

  ```js
  getComputedStyle(element).getPropertyValue("--color");
  ```
* Great for theming, dark mode, or data-driven styling.



✅ **In short:**
CSS custom properties make styles **reusable, dynamic, and maintainable**, especially when combined with `@property` and JavaScript.


