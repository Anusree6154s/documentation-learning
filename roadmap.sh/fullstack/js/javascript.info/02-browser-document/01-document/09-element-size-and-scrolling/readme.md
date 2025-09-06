

# 📏 Element Size and Scrolling in JavaScript

## 1. Key Geometry Properties

* **offsetParent** → nearest positioned ancestor (`absolute`, `relative`, `fixed`, `sticky`) or `<td>`, `<th>`, `<table>`, `<body>`.
* **offsetLeft / offsetTop** → coordinates relative to `offsetParent`.
* **offsetWidth / offsetHeight** → outer size (content + padding + border + scrollbar).
* **clientLeft / clientTop** → size of left/top border (also includes scrollbar width in RTL layouts).
* **clientWidth / clientHeight** → content + padding (❌ excludes border, ❌ excludes scrollbar).
* **scrollWidth / scrollHeight** → full content size (including hidden/scrolled-out parts).
* **scrollLeft / scrollTop** → how much scrolled from the left/top (✅ can be modified).

<br>

## 2. Important Notes

* Geometry properties return **numbers in px**.
* Geometry values = `0` (or `null` for `offsetParent`) if element is `display: none` or not in the document.
* **Do not use `getComputedStyle().width/height` for sizes**:

  * May return `auto`.
  * Affected by `box-sizing`.
  * Cross-browser differences (scrollbar handling).
* ✅ Use geometry props (`clientWidth`, `offsetWidth`, etc.) for reliable pixel sizes.

<br>

## 3. Tasks & Solutions

### 📝 Task 1: Scroll from the bottom

```js
let scrollBottom = elem.scrollHeight - elem.scrollTop - elem.clientHeight;
```

* Returns remaining scroll distance to bottom.
* ✅ 0 if fully scrolled down or no scroll.

<br>

### 📝 Task 2: Scrollbar width

```js
function getScrollbarWidth() {
  return window.innerWidth - document.documentElement.clientWidth;
}
```

* Works in any document.
* Returns `0` if scrollbar doesn’t take space (overlay scrollbars).

<br>

### 📝 Task 3: Place ball in center of field

```js
let fieldCoords = field.getBoundingClientRect();

ball.style.left = field.clientWidth / 2 - ball.offsetWidth / 2 + "px";
ball.style.top  = field.clientHeight / 2 - ball.offsetHeight / 2 + "px";
```

* Uses client sizes for field.
* Works with any ball/field size.

<br>

### 📝 Task 4: CSS width vs clientWidth (differences)

1. `getComputedStyle(elem).width` → CSS value (`auto`, `%`, etc.).
   `clientWidth` → exact px number.
2. `getComputedStyle().width` depends on **box-sizing**.
   `clientWidth` → always content + padding – scrollbar.
3. Cross-browser differences: scrollbar included/excluded inconsistently in CSS width.
   `clientWidth` → consistent.

