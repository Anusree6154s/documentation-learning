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
