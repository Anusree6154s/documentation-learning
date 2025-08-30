>[!NOTE]
>Notes only on topics I dont remember<br>
>Website: [web.dev/css](https://web.dev/learn/css/), summarised by gpt

<br>

## Topics
1. [box-model](#box-model)
2. selectors
3. nesting
4. [cascade](#cascade)
5. [inheritance](#inheritance)
6. [colors](#colors)
7. [sizing units](#sizing-units)

<br>

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

<br>

## Cascade
### 1. **Cascade Algorithm Steps**

The cascade decides which CSS rule wins when multiple rules apply.
The order of evaluation is:

1. **Position and Order of Appearance**

   * <mark>Later rules override earlier ones</mark> (if everything else is equal).
   * Applies to `<link>`, `<style>`, inline styles, and multiple declarations in the same block.

2. **Specificity**

   * <mark>More specific selectors override less specific ones.</mark>
   * Specificity hierarchy:

     * Inline styles (highest normal specificity)
     * IDs
     * Classes, attributes, pseudo-classes
     * Elements, pseudo-elements (lowest)
   * Specificity is cumulative (multiple selectors add up).

3. **Origin** (<mark>where styles come from</mark>)

   * Lowest → Highest:

     * User agent (browser defaults)
     * Local user styles
     * Author styles (you write them)
     * Author `!important`
     * User `!important`
     * User agent `!important`

4. **Importance**

   * <mark>Order of importance</mark> (lowest → highest):

     * Normal rules
     * Animations
     * `!important` rules
     * Transitions (highest when active)



### 2. **Position & Order Examples**

* Last declaration wins if specificity is equal:

  ```css
  button { color: red; }
  button { color: blue; } /* wins */
  ```
* Inline `style` attributes override external/embedded CSS (but still follow order if multiple values inside).
* Multiple declarations of same property → last valid one wins (useful for fallbacks):

  ```css
  .el {
    font-size: 1.5rem;
    font-size: clamp(1.5rem, 1rem + 3vw, 2rem); /* wins if supported */
  }
  ```


### 3. **Specificity Examples**

* Class beats element:

  ```css
  .my-element { color: red; }  /* wins */
  h1 { color: blue; }
  ```
* ID beats class or element.
* Long selector lists accumulate specificity → harder to override.


### 4. **Origin Example**

* Example priority (lowest → highest):

  * Browser default: `h1 { margin-block-start: 0.83em; }`
  * Framework (e.g. Bootstrap): `h1 { margin-block-start: 20px; }`
  * Author style: `h1 { margin-block-start: 2ch; }`
  * Media query: `h1 { margin-block-start: 1ch; }`
  * User custom style with `!important`: `h1 { margin-block-start: 2rem !important; }` → **this wins**



### 5. **Importance**

* Active transitions > active animations > `!important` > normal rules.
* Animations and transitions can temporarily override even `!important`.

### 6. Diff between author and user
* Diff
  * **Author = developer of the website**
  * **User = person visiting the site**
  * **User `!important` > Author `!important`** (because the user’s needs take priority).
* Diff in styles
  * **Author styles** = what *you* (developer) provide.
  * **User styles** = what *the visitor or browser* provides.
    * Custom stylesheets/extensions (like Stylish, Stylus, or uBlock cosmetic filters).
    * Browser accessibility settings (e.g. increasing default font size, forcing dark mode).


- Example:

```css
/* Author style */
h1 { font-size: 2rem; }

/* User style (via browser extension or OS setting) */
h1 { font-size: 1.2rem !important; } /* wins */
```
<br>

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

  <br>

  ## Colors

### Choosing Colors

* **Named Colors** → 148 options (`red`, `blue`, `goldenrod`, etc.)
* **Numeric Colors**

  * **Hex**: `#b71540` (most popular), supports alpha with 8 digits (`#00000080` = 50% transparent black).
  * **RGB**: `rgb(183 21 64)` or with alpha `rgb(0 0 0 / 50%)`.
  * **HSL**: `hsl(344 79% 40%)` or with alpha `hsl(0 0% 0% / 50%)`.

### Advanced Color Spaces

* **color() function** → Define in specific spaces:

  * `color(srgb 0.9 0.2 0.4)`
  * `color(display-p3 0.9 0.2 0.4)` (50% more colors than sRGB).
* **Oklab**: `oklab(75% 0.1 0.1)` (lightness + chroma channels).
* **OkLCh**: `oklch(80% 0.1 200)` (lightness, chroma, hue).

### System & Special Colors

* **transparent** → fully transparent.
* **currentColor** → inherits element’s text color.
* **System keywords** → OS-level colors like `Highlight`, `ButtonBorder`.

### <mark>Manipulating Colors</mark>

* **color-mix()** → <mark>Mix 2 colors</mark> (`color-mix(in srgb, red 40%, blue)`).
* **Relative color syntax** → <mark>Modify from a base color</mark>:

  ```css
  color: oklch(from red calc(l/2) c h);
  ```

  (halves lightness, keeps chroma, hue unchanged).

### Out of Gamut Colors

* If a screen can’t display a wide-gamut color → **gamut mapping** chooses the closest possible color.
* Use `@media (color-gamut: p3)` to control behavior.

### Where Colors Apply

* **Text**: `color`, `text-shadow`, `text-decoration-color`.
* **Backgrounds**: `background`, `background-color`, gradients.
* **Borders/outlines**: `border-color`, `outline-color`.
* **Shadows**: `box-shadow`.



✅ **Valid color examples:**

* `hsl(180deg 50% 50%)`
* `hotpink`
* `rgb(255, 0, 0)`
* `#0f08`

❌ **Invalid examples:**

* `rbga(400 0 1)`
* `#OOFZ2`
* `hsl(0, 0, 0)` (wrong format).


<br>

## Sizing Units
Perfect — let me turn that big chunk into **clean bullet points / cheat sheet style notes** 👇

---

# 📏 CSS Sizing Units – Cheat Sheet

## 🔢 Numbers

* **Unitless numbers** → used in opacity, line-height, rgb, filters, transform.

  * `line-height: 1.5;` → 150% of font size (good practice to keep unitless).
  * `opacity: 0.5;` → 50% opacity.
  * `scale(1.2)` → scales to 120%.
  * `rgb(50,50,50)` → grayscale.

---

## 📊 Percentages (%)

* Calculated relative to **something else** (depends on property):

  * `width: 50%` → relative to parent’s width.
  * `padding/margin: 50%` → relative to parent’s width (always, even vertical).
  * `transform: translateX(10%)` → relative to element’s own size.

---

## 📐 Dimensions & Lengths

* A **dimension** = number + unit → `1rem`, `20px`, `5cm`.

### Absolute Units (fixed sizes, best for print)

* `cm` → centimeters, 1cm = 96px / 2.54
* `mm` → millimeters, 1mm = 1/10 cm
* `Q` → quarter millimeters (1/40 cm)
* `in` → inches, 1in = 2.54cm = 96px
* `pc` → picas, 1pc = 1/6 in
* `pt` → points, 1pt = 1/72 in
* `px` → pixels, 1px = 1/96 in

### Relative Units (flexible, responsive)

* **Font-relative**

  * `em` → relative to parent’s font size.
  * `rem` → relative to root (`html`) font size.
  * `ex` → x-height of font (“x”).
  * `rex` → ex of root element.
  * `cap` → height of capital letters.
  * `rcap` → root capital height.
  * `ch` → width of "0".
  * `rch` → root ch value.
  * `ic` → width of full-width CJK glyph (“水”).
  * `ric` → root ic value.
  * `lh` → element’s line height.
  * `rlh` → root’s line height.

* **Viewport-relative**

  * `vw` → 1% of viewport width.
  * `vh` → 1% of viewport height.
  * `vi` → 1% of viewport inline axis (depends on writing mode).
  * `vb` → 1% of viewport block axis.
  * `vmin` → 1% of smaller dimension.
  * `vmax` → 1% of larger dimension.

* **Alt viewport units** (account for browser UI bars in mobile):

  * `lv*` → large viewport (UI hidden).
  * `sv*` → small viewport (UI visible).
  * `dv*` → dynamic viewport (changes with UI showing/hiding).

* **Container-relative** (work inside container queries):

  * `cqw` → 1% of container width.
  * `cqh` → 1% of container height.
  * `cqi` → 1% of inline axis.
  * `cqb` → 1% of block axis.
  * `cqmin` → 1% of smaller dimension.
  * `cqmax` → 1% of larger dimension.



###  Misc Units

* **Angles** → `deg`, `rad`, `grad`, `turn`.

  * Example: `rotate(60deg)` or `rotate(0.5turn)`.
* **Resolution** → `dpi`, `dpcm`, `dppx`.

  * Used in media queries to detect high-res displays (e.g. Retina).
  * Perfect question — this is a **practical use case of resolution units** in CSS. Let’s break it down 👇

---

## 1. **Resolution units**

* `dpi` = dots per inch
* `dpcm` = dots per centimeter
* `dppx` = dots per CSS pixel (relative to 1px at 96dpi → so `1dppx = 96dpi`)

They are most often used in **media queries** to check whether the display has a high pixel density.

---

## 2. **Why?**

High-DPI displays (e.g. Retina, 4K phones) pack more device pixels into the same CSS pixel size. If you serve a normal-resolution image, it looks **blurry**.
So you check resolution → then serve higher-res assets.

---

## 3. **Examples**

### Detect Retina (2× resolution) using `dppx`

```css
@media (min-resolution: 2dppx) {
  .logo {
    background-image: url("logo@2x.png");
  }
}
```

➡️ If the screen has at least **2 device pixels per CSS pixel**, use a higher-resolution image.

---

### Using `dpi`

```css
@media (min-resolution: 192dpi) {
  .logo {
    background-image: url("logo@2x.png");
  }
}
```

* `192dpi` is equivalent to `2dppx` because `1dppx = 96dpi`.

---

### Using `dpcm`

```css
@media (min-resolution: 75dpcm) {
  .logo {
    background-image: url("logo@2x.png");
  }
}
```

* `75dpcm` ≈ `192dpi`.

---

## 4. **Cross-browser compatibility**

For Safari and older browsers, you sometimes need **vendor-prefixed queries (browser specific css instead of a standard css for all types of browser)**:

```css
@media 
  (-webkit-min-device-pixel-ratio: 2), /* old Safari */
  (min-resolution: 192dpi),            /* dpi */
  (min-resolution: 2dppx) {            /* modern */
  
  .logo {
    background-image: url("logo@2x.png");
  }
}
```
 **In short:**
You use `dpi`, `dpcm`, or `dppx` inside `@media` queries to detect when a device has a **high pixel density display** and swap in higher-resolution assets (images, icons, etc.) to keep them sharp.


### <mark> Key Best Practices</mark>

* <mark>Use **relative units** (`em`, `rem`, `vw`, `ch`) → responsive, respects user preferences.</mark>
* <mark>Avoid **px for font-size** → ignores system/user settings.</mark>
* <mark>Use **absolute units** mainly for print</mark>.
  * “Print” = when your page is being **printed on paper** or viewed in a **print stylesheet** (e.g. `@media print`).
  * In this context, absolute physical units (`cm`, `mm`, `in`, `pt`, `pc`) are useful → they map to real-world sizes (e.g. exactly 10cm wide box on paper).
  
  👉 Example:
  
  ```css
  @media print {
    .ticket {
      width: 10cm;  /* will really be ~10cm wide on paper */
      height: 5cm;
    }
  }
  ```
* Use `ch` or `lh` for text width/line spacing control.
