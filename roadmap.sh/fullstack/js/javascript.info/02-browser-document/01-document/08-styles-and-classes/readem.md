

# 🎨 Styles and Classes in JavaScript

## 1. Ways to Style Elements

* **CSS class** → `<div class="box">` (preferred).
* **Inline style** → `<div style="color: red">`.
* ✅ Use **classes for static styles**.
* ✅ Use **inline styles for dynamic calculations** (e.g., `elem.style.left = "100px"`).

<br>

## 2. Managing Classes

### `className`

* Represents **entire class string**.
* Replaces all existing classes if assigned.

  ```js
  elem.className = "highlight";
  ```

### `classList` (preferred for individual changes)

* `elem.classList.add("class")` → add class.
* `elem.classList.remove("class")` → remove class.
* `elem.classList.toggle("class")` → toggle class on/off.
* `elem.classList.contains("class")` → check existence.
* `for (let c of elem.classList)` → iterate classes.

<br>

## 3. Managing Inline Styles

### `elem.style.property`

* Style properties use **camelCase**:

  * `background-color` → `elem.style.backgroundColor`.
  * `z-index` → `elem.style.zIndex`.
* Example:

  ```js
  elem.style.backgroundColor = "yellow";
  ```

### Resetting Styles

* To **remove** a style:

  ```js
  elem.style.display = "";
  elem.style.removeProperty("background");
  ```

### `cssText`

* Assign all styles as one string.

  ```js
  elem.style.cssText = `
    color: red;
    background: yellow;
    width: 100px;
  `;
  ```
* ⚠️ Replaces all existing inline styles.

<br>

## 4. Units in Styles

* Must include **CSS units** (`px`, `%`, `em`, etc.).

  ```js
  elem.style.margin = "20px"; // ✅ works
  elem.style.margin = 20;     // ❌ ignored
  ```

<br>

## 5. Computed Styles

### `getComputedStyle(elem, [pseudo])`

* Returns **resolved (final) styles** after CSS cascade.
* Example:

  ```js
  let style = getComputedStyle(elem);
  console.log(style.marginTop); // e.g., "5px"
  ```
* Always request **full property names** (`marginTop`, not `margin`).

### Limitations

* `:visited` styles are **hidden** (privacy protection).
* Computed values may be absolute (`px`) even if CSS used relative units (`em`, `%`).

<br>

## 6. Summary

* **Classes**:

  * `className` → replace full list.
  * `classList` → add/remove/toggle individual classes.
* **Styles**:

  * `style.property` → inline styles.
  * `cssText` → set all at once.
* **Reset**:

  * `style.prop = ""` or `style.removeProperty("prop")`.
* **Reading styles**:

  * `getComputedStyle()` → resolved values with cascade.

<br>

## 7. Task: Show Notification

### Requirement

Create `showNotification(options)` → shows a message in top-right corner, disappears after 1.5s.

### Example:

```js
function showNotification({top = 0, right = 0, html, className}) {
  let div = document.createElement("div");
  div.className = "notification " + (className ?? "");
  div.style.top = top + "px";
  div.style.right = right + "px";
  div.innerHTML = html;

  document.body.append(div);

  setTimeout(() => div.remove(), 1500);
}

// Usage:
showNotification({
  top: 10,
  right: 10,
  html: "Hello!",
  className: "welcome"
});
```
