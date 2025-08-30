
##  Pseudo-elements

* Allow you to **style parts of an element** or insert **virtual elements** without extra HTML.
* Written with `::` (e.g., `::before`, `::first-letter`).


<br>

##  Common Pseudo-elements

### 1. **`::before` & `::after`**

* Create virtual child elements.
* <mark>Require `content` property (string, image, counter, etc.).</mark>
* <mark>Don’t work on replaced elements (`<img>`, `<input>`, `<video>`), except `input[type="checkbox"]`.</mark>

```css
.my-element::before { content: "→ "; }
.my-element::after  { content: " ✓"; }
```

<br>


### 2. <mark>**`::first-letter`**</mark>

* <mark>Styles the **first letter** of block-level text (like a drop cap).</mark>
* Only supports limited properties:

  * color, background, border, float, font, some text properties.

```css
p::first-letter {
  font-size: 2.6em;
  font-weight: bold;
  color: blue;
}
```
<img width="128" height="74" alt="image" src="https://github.com/user-attachments/assets/f6d79e8a-88ba-45ea-a909-f548c983aaaf" />


<br>


### 3. <mark>**`::first-line`**</mark>

* <mark>Styles the **first line** of text (depends on line wrapping).</mark>
* Works on block/inline-block/list-item/table-caption/table-cell.
* Limited properties: color, background, font, text.

```css
p::first-line { font-weight: bold; }
```

<br>


### 4. <mark>**`::backdrop`**</mark>

* <mark>Styles the **background area** when an element is in **fullscreen**</mark> (e.g., `<dialog>`, `<video>`).

```css
video::backdrop { background: goldenrod; }
```
<br>



### 5. <mark>**`::marker`**</mark>

* <mark>Styles **list bullets/numbers** or the **arrow** in `<summary>`.</mark>
* Limited properties: color, content, whitespace, font, animation.

```css
ul::marker { color: hotpink; }
summary::marker { content: "➕ "; }
details[open] summary::marker { content: "➖ "; }
```
<br>



### 6. <mark>**`::selection`**</mark>

* <mark>Styles **highlighted text**</mark> (when user selects with mouse/keyboard).
* Limited properties: color, background-color, text.

```css
::selection { background: green; color: white; }
```
<br>



### 7. **`::placeholder`**

* Styles the **placeholder text** in inputs.
* Limited properties: color, background, font, text.

```css
input::placeholder { color: darkcyan; }
```
<br>



### 8. <mark>**`::cue`**</mark>

* Styles <mark>**captions**</mark> (WebVTT) in `<video>`.
* Can target specific tags inside captions.

```css
video::cue { color: yellow; }
video::cue(b) { color: red; }
```



## ✅ Summary

* Pseudo-elements help style **sub-parts** of an element or add **virtual elements**.
* Many have **restricted CSS property support**.
* Useful for: decoration, accessibility, styling specific text fragments, and internationalization.
