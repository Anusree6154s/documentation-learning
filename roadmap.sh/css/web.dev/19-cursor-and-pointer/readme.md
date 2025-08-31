
## 🖱️ Cursors & Pointers in CSS

### **1. Cursors**

* Browsers change cursors automatically depending on context:

  * Default arrow → general use.
  * I-beam → over text (selectable).
  * Hand (pointer) → over links or clickable elements.
* Developers can **customize cursors** with the `cursor` property.
* Options:

  * Keywords (e.g., `pointer`, `move`, `grab`, `resize`).
  * Custom images (`cursor: url(my-cursor.png), auto;`).

<br>

### <mark>**2. Carets**</mark>

* **Caret ≠ cursor** → shows text insertion position in editable fields.
* Style it with:

  ```css
  input, textarea {
    caret-color: red;
  }
  ```
  <img width="356" height="70" alt="image" src="https://github.com/user-attachments/assets/aebdd023-9a10-4575-b4dd-3e896d151979" />

<br>



### **3. Responding to Pointer Inputs**

* **Precision varies**:

  * Mouse / trackpad → *fine precision*.
  * Touchscreen → *coarse precision*.
* Accessibility tip → make **buttons/targets large enough** and not too close together.

<br>


### **4. Media Queries for Pointers**

* `pointer` → describes the **primary** input device.
* <mark>`any-pointer` → checks **all available devices**.</mark>
* <mark>Values:</mark>

  * `fine` → precise (mouse, stylus).
  * `coarse` → less precise (touchscreen).
  * `none` → no pointing device.

Example:

```css

 /* Fine pointer (mouse, stylus) */
      @media (pointer: fine) {
        .box {
          background: #e0f7ff;
        }
        .box::after {
          content: " (fine: mouse or stylus)";
        }
      }

      /* Coarse pointer (touchscreen) */
      @media (pointer: coarse) {
        .box {
          background: #ffe0e0;
        }
        .box::after {
          content: " (coarse: touchscreen)";
        }
      }

      /* No pointer device (TV, voice) */
      @media (pointer: none) {
        .box {
          background: #e0ffe0;
        }
        .box::after {
          content: " (none: no pointer device)";
        }
      }

      /* Any-pointer checks all available input devices */
      @media (any-pointer: coarse) {
        .box {
          border-color: orange;
        }
      }
```

<br>


### <mark>**5. Touch Gestures**</mark>

* Browsers handle gestures by default (pinch-zoom, double-tap, etc.).
* Control them with `touch-action`:

  * `pan-x` → allow horizontal scrolling.
  * `pan-y` → allow vertical scrolling.
  * `pinch-zoom` → allow zooming.
  * `manipulation` → shortcut for `pan-x pan-y pinch-zoom`.
* ⚠️ Be careful: disabling zoom may reduce accessibility.

<br>


### **6. Disabling Interactions**

* Use `pointer-events: none;` to make an element completely non-interactive (no hover, no click).

