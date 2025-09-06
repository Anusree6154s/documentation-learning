
# 📍 Coordinates in JavaScript

### 🔹 Coordinate Systems

* **Window-relative (clientX/clientY)**

  * Measured from **window’s top-left corner**.
  * Similar to `position:fixed`.
* **Document-relative (pageX/pageY)**

  * Measured from **document’s top-left corner**.
  * Similar to `position:absolute`.
* At scroll = 0 → both systems are equal.
* After scroll →

  * `pageX/pageY` stays the same.
  * `clientX/clientY` changes.

<br>

### 🔹 Element Coordinates

* `elem.getBoundingClientRect()` → gives **window coordinates** of element’s bounding box.
* Returns a `DOMRect` object with:

  * **Basic:** `x`, `y`, `width`, `height`.
  * **Derived:** `top`, `bottom`, `left`, `right`.
* Notes:

  * Coordinates can be **fractions** (e.g. `10.5`).
  * Can be **negative** if element is scrolled out of view.
  * Internally `left = x`, `top = y`, etc.

<br>

### 🔹 Cross-browser Notes

* IE does **not support `x/y`**, only `top/left`.
* `width/height` may theoretically be negative (for “reverse” rectangles), but in practice are always positive.

<br>

### 🔹 elementFromPoint(x, y)

* Returns **most nested element** at given window coordinates.
* Example:

  ```js
  let elem = document.elementFromPoint(x, y);
  ```
* If coordinates are **outside viewport** → returns `null`.
* Useful for detecting which element is at the center/mouse position.

<br>

### 🔹 Positioning Elements

* **Using `position:fixed` (window-based):**

  ```js
  coords = elem.getBoundingClientRect();
  message.style.left = coords.left + "px";
  message.style.top  = coords.bottom + "px";
  ```

  ⚠️ Message “runs away” when scrolling.

* **Using `position:absolute` (document-based):**

  ```js
  function getCoords(elem) {
    let box = elem.getBoundingClientRect();
    return {
      top: box.top + window.pageYOffset,
      left: box.left + window.pageXOffset
    };
  }
  ```

  ✅ Message **stays near element** while scrolling.

<br>

### 🔹 Conversion Formula

* To switch between systems:

  ```
  pageY = clientY + window.pageYOffset
  pageX = clientX + window.pageXOffset
  ```

<br>

### 🔹 Summary

* `clientX/Y` → window coords → good for `position:fixed`.
* `pageX/Y` → document coords → good for `position:absolute`.
* `getBoundingClientRect()` → base method for window coords.
* `elementFromPoint()` → find element at specific coords.
* Always adjust with `pageXOffset/pageYOffset` for document-based positioning.
