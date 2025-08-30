## Box Model

### Why width looks “wrong”

* By default, CSS uses **content-box** sizing.
* That means when you set `width` and `height`, they apply only to the **content box** (the text or child elements).
* **Padding** and **border** are then *added* on top of that width/height → making the element bigger than you expected.

Example:

```css
p {
  width: 100px;
  height: 50px;
  padding: 20px;
  border: 1px solid;
}
```

→ Actual width = 100 (content) + 40 (padding) + 2 (border) = **142px**



### Intrinsic vs. Extrinsic sizing
* <mark>**Extrinsic sizing**: You set a fixed size (`width`, `height`).</mark>

  * Example: `width: 400px;`
  * Risk: content may **overflow** if it doesn’t fit.
* <mark>**Intrinsic sizing**: Browser decides size based on content. (default)</mark>

  * Example: <mark>`width: min-content;`</mark>
  * The box grows/shrinks to fit the content → less chance of overflow.



### Overflow

* Happens when content is **too large** for the box.
* Controlled with the `overflow` property (`visible`, `hidden`, `scroll`, `auto`).



### 4 areas of the Box Model

1. **Content box** – holds text or children.
2. **Padding box** – space inside, around the content (background is visible here).
3. **Border box** – surrounds padding/content, visible border line.
4. **Margin box** – space outside the element (between other elements).

(Analogy: artwork → content, white mat → padding, frame → border, space between frames → margin.)



### Defaults (User Agent Styles)

* Browsers apply default styles (user agent stylesheet).
* Examples:

  * `<div>` → `display: block`
  * `<span>` → `display: inline`
  * `<li>` → `display: list-item`
* Default **box-sizing**: `content-box`.



### box-sizing property

* <mark> **`box-sizing: content-box`** (default) → width applies to **content only**. Makes boxes bigger than expected </mark> Padding & border add to total size.
* <mark> **`box-sizing: border-box`** → width applies to **border box** (includes, <ins>padding + border</ins>). </amrk> More predictable.
* <img width="564" height="282" alt="image" src="https://github.com/user-attachments/assets/68d90919-5bc8-4da9-b126-cb24f3830bd3" />


Example:

```css
.my-box {
  width: 200px;
  padding: 20px;
  border: 10px solid;
}
```

* With `content-box`: 200 + 40 + 20 = **260px** wide.
* With `border-box`: total stays **200px** wide.



### Common practice

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

* Applies the **border-box model globally**.
* Makes layouts more predictable and easier to manage.



✅ **Summary**:

* Every element is a box (even text).
* The box has 4 parts: content, padding, border, margin.
* Default sizing (`content-box`) can make boxes bigger than expected.
* `border-box` sizing fixes this by including padding/border inside the width/height.
* Use DevTools’ box model debugger to visualize calculations.
