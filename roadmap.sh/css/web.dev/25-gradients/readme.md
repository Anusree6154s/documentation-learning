

## 🎨 CSS Gradients 

### 🔹 General

* A **gradient is treated like an image** → can be used anywhere `background-image` works.
* Created with `linear-gradient()`, `radial-gradient()`, or `conic-gradient()`.
* Can blend multiple colors, angles, and positions.
* Gradients can be **layered** by separating them with commas.

<br>

### 🔹 Linear Gradients

* Created with `linear-gradient()`.
* Transition between colors in a straight line.
* Default direction = **top → bottom**.
* You can specify:

  * **Angles** (`45deg`, `90deg`, etc.).
  * **Directions** with keywords (`to right`, `to bottom left`).
  * **Color stops** → define where colors start/stop (`darkred 30%, crimson`).
* Example:

  ```css
  background: linear-gradient(to right, black, white);
  ```

<br>

### 🔹 Radial Gradients

* Created with `radial-gradient()`.
* Colors radiate from a center point outward.
* Default: circle/ellipse at the center → extends to the farthest corner.
* Shape & size options:

  * `circle` / `ellipse`.
  * `closest-side`, `closest-corner`, `farthest-side`, `farthest-corner`.
* Example:

  ```css
  background: radial-gradient(circle, white, black);
  ```

<br>

### 🔹 Conic Gradients

* Created with `conic-gradient()`.
* Colors rotate **around a center point (360°)**.
* Start angle defaults to `0deg` (top).
* Position defaults to `center`.
* Good for **pie charts, color wheels, dials**.
* Example:

  ```css
  background: conic-gradient(white, black);
  ```

<br>

### 🔹 <mark>Repeating Gradients</mark>

* Functions:

  * `repeating-linear-gradient()`
  * `repeating-radial-gradient()`
  * `repeating-conic-gradient()`
* Repeat patterns if gradient length allows.
* Used for stripes, grids, textures.
* Example (striped background):

  ```css
  background: repeating-linear-gradient(
    45deg,
    red,
    red 30px,
    white 30px,
    white 60px
  );
  ```

<br>

### 🔹 Mixing Gradients

* Multiple gradients can be stacked:

  ```css
  background: linear-gradient(to right, red, blue),
              radial-gradient(circle, yellow, transparent);
  ```

<br>

### 🔹 <mark>Color Interpolation & Spaces</mark>

* Gradients interpolate between colors.
* <mark>Tnterpolation means how the browser calculates the in-between colors when blending from one color stop to another.</mark>
* You can <mark>control interpolation using **color spaces** (`srgb`, `hsl`, `oklab`, `oklch`).</mark>
* Options:

  * `in oklch` → produces vibrant, safer blends.
  * `increasing hue` / `decreasing hue` → control direction around color wheel.
  * `shorter` / `longer hue` → control whether gradient takes shortest or longest path.
* Example:

  ```css
  background: linear-gradient(in oklch increasing hue, deeppink, yellow);
  ```

## Examples
<details>
  <summary>Code</summary>
  
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS Gradients Demo</title>
  <style>
    body {
      font-family: sans-serif;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      padding: 20px;
      background: #f9f9f9;
    }

    .box {
      height: 180px;
      border-radius: 12px;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      text-shadow: 0 1px 2px rgba(0,0,0,0.6);
    }

    /* Linear */
    .linear {
      background: linear-gradient(to right, darkviolet, violet);
    }

    /* Radial */
    .radial {
      background: radial-gradient(circle, yellow, orange, red);
      color: black;
    }

    /* Conic */
    .conic {
      background: conic-gradient(cyan, magenta, yellow, cyan);
    }

    /* Repeating Linear */
    .repeating-linear {
      background: repeating-linear-gradient(
        45deg,
        red,
        red 20px,
        white 20px,
        white 40px
      );
      color: black;
    }

    /* Repeating Radial */
    .repeating-radial {
      background: repeating-radial-gradient(circle,
        blue 0px, blue 10px,
        white 10px, white 20px
      );
      color: black;
    }

    /* Repeating Conic */
    .repeating-conic {
      background: repeating-conic-gradient(
        from 0deg,
        lime 0deg 20deg,
        white 20deg 40deg
      );
      color: black;
    }

    /* Mixed */
    .mixed {
      background: 
        linear-gradient(to right, rgba(255,0,0,0.6), rgba(0,0,255,0.6)),
        radial-gradient(circle at center, yellow, transparent);
    }

    .my-box {
        background: linear-gradient(red, blue);
      }

    /* Color spaces */
    .color-space {
      background: linear-gradient(in oklch increasing hue, deeppink, yellow);
    }
  </style>
</head>
<body>
  <div class="box linear">Linear Gradient</div>
  <div class="box radial">Radial Gradient</div>
  <div class="box conic">Conic Gradient</div>
  <div class="box repeating-linear">Repeating Linear</div>
  <div class="box repeating-radial">Repeating Radial</div>
  <div class="box repeating-conic">Repeating Conic</div>
  <div class="box mixed">Mixed Gradients</div>
  <div class="box my-box">Color Space Gradient without interpolate</div>
  <div class="box color-space">Color Space Gradient</div>
</body>
</html>
```
</details>


<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/da095339-8d40-45a5-879b-12ee6ebfee23" />

<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/6357e86d-4c81-4c6d-88fd-9801695de37f" />



✅ This page shows:

* Linear
* Radial
* Conic
* Repeating (linear, radial, conic)
* Mixed gradients
* Gradient without  **color space interpolation**
* Gradient with **color space interpolation**

<br>
  
## <mark>Interpolation</mark>

In **CSS gradients**, **interpolation** means:
👉 *How the browser calculates the in-between colors when blending from one color stop to another.*

<br>

### 🔹 Example: No interpolation vs interpolation

If you write:

```css
.my-box {
  background: linear-gradient(red, blue);
}
```

* You have **two stops**: red (start) → blue (end).
* The browser **interpolates** (calculates all colors in between).

  * So at 50% you’ll see **purple** (a mix of red + blue).
  * At 25% you’ll see a reddish-purple, etc.

<br>

### 🔹 Different interpolation modes

CSS lets you choose **how the blending is done** using **color spaces**:

```css
.my-box {
  background: linear-gradient(in oklch, deeppink, yellow);
}
```

* `in oklch` → tells the browser to interpolate using the **OKLCH color space**.
* This can produce smoother, more natural blends compared to default **sRGB**.

<br>

### 🔹 Cylindrical color spaces (HSL, LCH, OKLCH)

These color models have a **hue circle** (like a color wheel).

* By default, interpolation takes the **shortest path** around the circle.
* You can force:

  * `increasing hue` → always clockwise around the wheel.
  * `decreasing hue` → always counter-clockwise.
  * `shorter` / `longer` → force the shorter or longer arc.

Example:

```css
.my-box {
  background: linear-gradient(in hsl longer hue, red, green);
}
```

* Instead of going directly from red → green, it may go the **long way around the color wheel**, passing through more hues.

<br>

✅ So in short:
**Interpolation = how colors are mixed between stops.**
Different **color spaces** (sRGB, HSL, LAB, OKLCH) and **hue directions** change the look of the gradient.
