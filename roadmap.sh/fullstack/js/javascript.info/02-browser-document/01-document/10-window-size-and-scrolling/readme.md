
### 📏 Geometry (sizes)

* **Visible window size (viewport, excluding scrollbar)**:
  `document.documentElement.clientWidth`
  `document.documentElement.clientHeight`

* **Full document size (including scrolled-out part)**:

  ```js
  let scrollHeight = Math.max(
    document.body.scrollHeight, document.documentElement.scrollHeight,
    document.body.offsetHeight, document.documentElement.offsetHeight,
    document.body.clientHeight, document.documentElement.clientHeight
  );
  ```

* **Difference from `window.innerWidth/innerHeight`**:

  * `innerWidth/innerHeight` → includes scrollbar.
  * `clientWidth/clientHeight` → excludes scrollbar (usually preferred for layout).

<br>

### 📜 Scrolling

* **Current scroll position**:

  * `window.pageXOffset` (alias `scrollX`) → horizontal scroll.
  * `window.pageYOffset` (alias `scrollY`) → vertical scroll.

* **Scroll page programmatically**:

  * `window.scrollTo(x, y)` → absolute position.
  * `window.scrollBy(dx, dy)` → relative movement.
  * `elem.scrollIntoView(top = true)` → scrolls element into view.

<br>

### 🚫 Disable scrolling

* To freeze page scroll:

  ```js
  document.body.style.overflow = "hidden"; // disable
  document.body.style.overflow = "";       // enable
  ```
* ⚠️ Scrollbar disappears → may cause layout shift (can be fixed with padding compensation).

<br>

✅ **Summary**

* Use `clientWidth/clientHeight` for viewport.
* Use `Math.max(…)` trick for full document size.
* Use `pageXOffset/pageYOffset` (or `scrollX/scrollY`) for scroll position.
* Use `scrollTo`, `scrollBy`, or `scrollIntoView` to scroll programmatically.
* Use `overflow: hidden` to lock scroll.
