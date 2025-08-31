

#  CSS Shadows

## 1. **Box Shadow (`box-shadow`)**

* Adds a shadow to the **box** of an element.
* Works on **block and inline** elements.
* Syntax:

  ```css
  box-shadow: [inset] x-offset y-offset blur-radius spread-radius color;
  ```

  * **x-offset** → horizontal shift (positive = right, negative = left).
  * **y-offset** → vertical shift (positive = down, negative = up).
  * **blur-radius** → bigger = more blurry.
  * **spread-radius** → expands/shrinks shadow size.
  * **color** → any valid CSS color.
  * `inset` → makes the shadow inside the box.

✅ Example:

```css
/* Outer shadow */
.my-box {
  box-shadow: 5px 5px 20px 5px #000;
}

/* Inner shadow */
.my-box {
  box-shadow: inset 5px 5px 20px 5px #000;
}
```

* **Multiple shadows**: comma-separated list.

```css
.my-box {
  box-shadow: 
    5px 5px 20px darkslateblue, 
    -5px -5px 20px dodgerblue,
    inset 0 0 10px darkslategray;
}
```

* **Affected by border-radius** → shadow follows rounded corners.
* **Clipped by parent `overflow: hidden`** → shadow won’t extend outside.

<br>

## 2. **Text Shadow (`text-shadow`)**

* Adds a shadow to **text only**.
* Syntax (same as box-shadow, but **no spread and no inset**):

  ```css
  text-shadow: x-offset y-offset blur-radius color;
  ```

✅ Example:

```css
.my-text {
  text-shadow: 3px 3px 3px hotpink;
}
```

* Shadows **not clipped** by text shape → shows through transparent text.
* Supports **multiple shadows** (comma-separated).
  ✅ Example for **3D effect**:

```css
.my-text {
  text-shadow:
    1px 1px 0 white,
    2px 2px 0 firebrick;
}
```

<br>


## 3. **Drop Shadow (`filter: drop-shadow()`)**

* Works on the **alpha mask** of an element (e.g., PNG cutout images).
* Perfect for **non-rectangular shapes** like product images.
* Syntax (similar to box-shadow, but **no spread, no inset**):

  ```css
  filter: drop-shadow(x-offset y-offset blur-radius color);
  ```

✅ Example:

```css
.my-image {
  filter: drop-shadow(0px 0px 10px rgba(0 0 0 / 30%));
}
```

* Can chain **multiple drop shadows**:

```css
.my-image {
  filter: drop-shadow(2px 2px 5px black)
          drop-shadow(-2px -2px 5px gray);
}
```

<br>


## 🔑 Quick Recap:

* <mark>**Box-shadow**</mark>
  - → shadows for **elements’ boxes**.
  - → <mark>puts the shadow around the *bounding box* of the image. If your PNG has transparency, the shadow is still a rectangle.</mark>
* **Text-shadow** → shadows for **text only**.
* <mark>**Drop-shadow (filter)**</mark>
  * → shadows that follow **transparent shapes/images**.
  * → <mark>applies the shadow only to the **visible pixels** (the alpha mask). For a cutout PNG (like the cat above), the shadow hugs the shape instead of a box.</mark>


