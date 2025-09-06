
### 1. Scroll Event

* `scroll` event fires when page or an element is scrolled.
* Works on `window` and scrollable elements.
* Example: show current scroll position

  ```js
  window.addEventListener('scroll', () => {
    showScroll.innerHTML = window.pageYOffset + 'px';
  });
  ```

<br>

### 2. Preventing Scroll

* `onscroll + preventDefault()` ❌ doesn’t work (fires **after** scroll).
* Must prevent events that cause scroll (e.g., `keydown` for PageUp/PageDown).
* More reliable → use CSS:

  ```css
  body { overflow: hidden; }
  ```

<br>

### 3. Tasks / Applications

#### A. Endless Page (infinite scroll)

* Append content when user reaches near page bottom.
* “Near bottom” = within \~100px of `document.documentElement.scrollHeight`.
* Used for “load more messages/goods”.

<br>

#### B. Up/Down Button (“Back to top”)

* Invisible if scroll < window height.
* Appears if scroll > window height.
* Clicking scrolls to top (`window.scrollTo(0, 0)`).

<br>

#### C. Lazy Load Images

* Start with placeholder:

  ```html
  <img src="placeholder.svg" data-src="real.jpg">
  ```
* On scroll, if image enters viewport → replace `src` with `data-src`.
* Images visible on load → load immediately.
* Once loaded → don’t reload again.
* Optimization: preload images **one screen ahead**.

<br>

### 4. Summary

* **Scroll event** is key for dynamic interfaces (lazy load, infinite content, sticky elements).
* To block scrolling, prevent it at the source (keys/touch), or use CSS.
* Common patterns: infinite scroll, back-to-top button, lazy loading.
