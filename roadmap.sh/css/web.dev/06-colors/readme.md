 ## Colors

### Choosing Colors

* **Named Colors** → 148 options (`red`, `blue`, `goldenrod`, etc.)
* **Numeric Colors**

  * **Hex** (Hexadecimal): `#b71540` (most popular), supports alpha with 8 digits (`#00000080` = 50% transparent black).
  * **RGB** (Red Green Blue): `rgb(183 21 64)` or with alpha `rgb(0 0 0 / 50%)`.
  * **HSL** (Hue Saturation Lightness.): `hsl(344 79% 40%)` or with alpha `hsl(0 0% 0% / 50%)`.
    * Hue (the color type), Saturation (the intensity or purity of the color), and Lightness (the brightness of the color).

### Advanced Color Spaces

* **color() function** → Define in specific spaces:

  * `color(srgb 0.9 0.2 0.4)`
  * `color(display-p3 0.9 0.2 0.4)` (50% more colors than sRGB).
* **Oklab**: `oklab(75% 0.1 0.1)` (lightness + chroma channels).
* **OkLCh**: `oklch(80% 0.1 200)` (lightness, chroma, hue).

### oklab vs oklch

- ####  `oklab()`
  
   * Function: `oklab(L a b)`
   * Channels:
   
     * **L** → Lightness (0% = black, 100% = white)
     * **a** → Green–Red axis (negative = greenish, positive = reddish)
     * **b** → Blue–Yellow axis (negative = bluish, positive = yellowish)
   * Example:
   
     ```css
     color: oklab(75% 0.1 0.1);
     ```
   
     → 75% lightness, slightly shifted toward red and yellow.
   
   * This is analogous to CIELAB (`lab()`), but tuned for better display behavior.



- ####  `oklch()`

  * Function: `oklch(L C h)`
  * Channels:
  
    * **L** → Lightness (same as OKLab)
    * **C** → Chroma (like saturation; 0 = gray, higher values = more vivid color)
    * **h** → Hue angle in degrees (0 = red, 120 = green, 240 = blue, etc.)
  * Example:
  
    ```css
    color: oklch(75% 0.2 40);
    ```
  
    → 75% lightness, 20% chroma, hue at 40° (orangey).
  
  * This is basically OKLab converted into polar coordinates (just like `lch()` is a polar version of `lab()`).

- ###  Why use them?

  * More perceptually uniform → changes in values match how humans *see* color changes.
  * Good for designing accessible color palettes, gradients, and contrasts.
  * Wide-gamut friendly (works with modern displays beyond sRGB).
  👉 Quick analogy:
  
  * `oklab()` = rectangular coordinates (X and Y axes for colors).
  * `oklch()` = polar coordinates (angle + distance from center).

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
- <mark>If a screen can’t display a wide-gamut color → **gamut mapping** chooses the closest possible color</mark>.
* Use `@media (color-gamut: p3)` to control behavior.

#### Gamut
* <mark>A gamut is simply the range of colors that a device or system can represent</mark>.
- Analogy:
  - Think of gamut as a box of crayons.
  - A cheap box (sRGB) has only basic colors.
  - A fancy artist’s box (P3/Rec.2020) has more shades.
  - If you ask for a neon marker that isn’t in your box, the system will pick the closest crayon you do have.

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
