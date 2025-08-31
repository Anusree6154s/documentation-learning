

### 📌 CSS Functions – Key Takeaways

**1. What is a function?**

* Named, self-contained piece of code that performs a task.
* Accepts arguments (inputs) and returns a value.
* In CSS, functions are built-in (cannot define your own).
* Many are **pure functions** → same input always gives the same output.

<br>

**2. Functional selectors**

* Functions like `:is()`, `:not()` → take selectors as arguments.

```css
.post :is(h1, h2, h3) { line-height: 1.2; }
```

<br>

**3. Custom properties & `var()`**

* CSS variables (`--base-color`) are referenced with `var()`.
* Can include a fallback:

```css
background: var(--base-color, hotpink);
```

<br>

**4. Value-returning functions**

* `var()` → returns a variable’s value.
* <mark>`attr()` → fetches an attribute.</mark>
* `url()` → references external resources.

<br>

**5. Color functions**

* Examples: `rgb()`, `hsl()`, `lab()`, `lch()`, `oklab()`, `color()`.

<br>

**6. Math functions**

* `calc()` → perform calculations with mixed units.
* `min()` / `max()` → pick smallest/largest value.
* <mark>`clamp(min, ideal, max)` → restrict within a flexible range.</mark>

<br>

**7. Trigonometric functions**

* `sin()`, `cos()`, `tan()` → use angles.
* Inverse: `asin()`, `acos()`, `atan()`, `atan2()`.
* `hypot()` → find hypotenuse length.

<br>

**8. Exponential functions**

* `pow(base, exponent)` → base^exponent.
* `exp(x)` → e^x.
* `sqrt(x)` → square root.
* `log(value, base)` → logarithm.

<br>

**9. Sign-related functions**

* `abs(x)` → absolute value.
* `sign(x)` → returns -1, 0, or 1.

<br>

**10. Shape functions**

* For clipping & text wrapping:

  * <mark>`circle()`, `ellipse()`, `inset()`, `polygon()`, `path()`.</mark>

<br>

**11. Transform functions**

* **Rotate:** `rotate()`, `rotateX()`, `rotateY()`, `rotate3d()`.
* **Scale:** `scale()`, `scaleX()`, `scaleY()`, `scale3d()`.
* **Translate:** `translate()`, `translateX()`, `translateY()`, `translate3d()`.
* **Skew:** `skew()`, `skewX()`, `skewY()`.
* **Perspective:** depth effect with `perspective`.

<br>

**12. Other categories**

* **Animations:** timing functions like `steps()` and `cubic-bezier()`.
* **Gradients:** `linear-gradient()`, `radial-gradient()`, `conic-gradient()`.
* **Filters:** `blur()`, `brightness()`, `contrast()`, etc.

<br>

✅ In short: **CSS functions are tools to compute values dynamically** → for sizes, colors, math, shapes, transforms, animations, and more.
