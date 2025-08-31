

## 🔹 CSS Blend Modes

### 1. **What are blend modes?**

* Define how two layers (backgrounds, images, or elements) mix together.
* Common in design tools (Photoshop, Figma) → also available in CSS.
* CSS properties:

  * `mix-blend-mode` → blends **entire element** with backdrop.
  * `background-blend-mode` → blends **multiple backgrounds** of one element.

<br>

### 2. **<mark>Categories of blend modes</mark>**

* **Separable** → works per RGB channel separately.
* **Non-separable** → works with overall color components (HSL-like: hue, saturation, luminosity).

<br>

### 3. **Separable blend modes**

* **normal** → default, no blending.
* **multiply** → darker result (whites disappear, blacks stay).
* **screen** → lighter result (inverse of multiply).
* **overlay** → mix of multiply + screen, boosts contrast.
* **darken** → keeps the darker color per channel.
* **lighten** → keeps the lighter color per channel.
* **color-dodge** → brightens backdrop to match source.
* **color-burn** → darker + more saturated mid-tones.
* **hard-light** → high-contrast version, depends on source brightness.
* **soft-light** → gentler overlay (softer contrast).
* **difference** → subtracts pixel values, inverts light areas.
* **exclusion** → like difference but softer (same colors → gray).

<br>

### 4. **Non-separable blend modes**

* **hue** → takes source hue + keeps backdrop saturation & luminosity.
* **saturation** → takes source saturation + keeps hue & luminosity.
* **color** → combines source hue & saturation + backdrop luminosity.
* **luminosity** → opposite of color (source luminosity + backdrop hue/saturation).

<br>

### 5. **Special property**

* `isolation: isolate;` → creates a **new stacking context** so the element doesn’t blend with backdrop.

  * Useful when you want blending only inside an element, not with parent layers.

<br>

### 6. **Use-cases**

* 🎨 Creative effects (duotone images, photo filters).
* ✨ UI polish (hover highlights, overlays).
* 🖼 Utilities (removing white backgrounds).

## Examples
<details>
  <summary>Code</summary>

  ```html
  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Blend Mode Examples</title>
  <style>
    .container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 20px;
      padding: 20px;
    }
    .box {
      position: relative;
      width: 250px;
      height: 150px;
      background: url('https://picsum.photos/id/1015/600/400') center/cover;
      border-radius: 10px;
      overflow: hidden;
      color: white;
      font-family: sans-serif;
      font-size: 14px;
      font-weight: bold;
      display: flex;
      align-items: flex-end;
      justify-content: center;
    }
    .overlay {
      position: absolute;
      inset: 0;
      background: rgba(255, 0, 0, 0.6);
    }
    .label {
      position: relative;
      padding: 5px 10px;
      background: rgba(0,0,0,0.4);
      border-radius: 4px;
      margin: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box"><div class="overlay" style="mix-blend-mode: normal"></div><div class="label">normal</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: multiply"></div><div class="label">multiply</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: screen"></div><div class="label">screen</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: overlay"></div><div class="label">overlay</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: darken"></div><div class="label">darken</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: lighten"></div><div class="label">lighten</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: color-dodge"></div><div class="label">color-dodge</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: color-burn"></div><div class="label">color-burn</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: hard-light"></div><div class="label">hard-light</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: soft-light"></div><div class="label">soft-light</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: difference"></div><div class="label">difference</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: exclusion"></div><div class="label">exclusion</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: hue"></div><div class="label">hue</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: saturation"></div><div class="label">saturation</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: color"></div><div class="label">color</div></div>
    <div class="box"><div class="overlay" style="mix-blend-mode: luminosity"></div><div class="label">luminosity</div></div>
  </div>
</body>
</html>

```
</details>

<img width="1105" height="671" alt="image" src="https://github.com/user-attachments/assets/aca69abb-eeee-44ed-8988-cd868e067c43" />
