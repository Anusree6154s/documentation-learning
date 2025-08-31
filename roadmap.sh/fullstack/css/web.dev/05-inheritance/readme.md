## Inheritance


* Some CSS properties **inherit automatically** from their parent elements.

### 1. **Common Properties that Inherit by Default**

Properties related to **text and font styling** (not box model).
Examples:

* `color`
* `font` (family, size, weight, style, variant)
* `line-height`
* `letter-spacing`, `word-spacing`
* `text-align`, `text-transform`, `text-indent`
* `visibility`, `cursor`, `quotes`, `list-style`

👉 <mark>Layout properties like `margin`, `padding`, `border`, `background` **do not inherit by default**</mark>.


### 2. **Computed Values**

* Each element always has **every CSS property** defined (either by inheritance, initial value, or cascade).
* If parent has `font-weight: bold`, all children inherit unless explicitly overridden.


### 3. **Keywords to Control Inheritance**

* **`inherit`** → Force property to take the parent’s value.

  ```css
  .my-component strong { font-weight: inherit; }
  ```

* **`initial`** → Reset property to CSS initial default value.

  ```css
  aside strong { font-weight: initial; } /* removes bold */
  ```

* **`unset`** → Acts as:

  * `inherit` if property normally inherits (e.g. `color`).
  * `initial` if property doesn’t inherit (e.g. `margin`).

  ```css
  aside p { margin: unset; color: unset; }
  ```

* **`all: unset`** → Reset *all properties* on an element.

  ```css
  aside p { all: unset; }
  ```

* **`revert`** → Undo **your authored styles** and fall back to **user-agent or user styles**.

  ```css
  aside p { padding: revert; }
  ```

* **`revert-layer`** → Undo styles in the **current cascade layer only**.
  Useful with 3rd-party libraries inside `@layer`.


### 4. **Inheritance Gotchas**

* Inheritance only goes **downward** (children get values, parents don’t).
* If you want to stop inherited styles → use `initial`, `unset`, or `revert`.
* If you want to guarantee consistency with parent styles → use `inherit`.

### 5. **Summary:**

* Inheritance saves you from repeating CSS.
* <mark>Not all properties inherit — mostly **text-related ones do**</mark>.
* Control inheritance with `inherit`, `initial`, `unset`, `revert`, and `revert-layer`.

  
