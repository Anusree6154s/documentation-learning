

## 🎨 CSS `filter` & `backdrop-filter`

### 🔹 What `filter` does

* Applies **visual effects** (blur, brightness, contrast, etc.) to an **element itself**.
* Affects **the whole element including text & content**.
* Multiple filters can be chained together.
* If any filter is invalid → **all filters fail**.

### 🔹 What `backdrop-filter` does

* Applies filters **only to what’s behind an element** (the backdrop).
* Great for **frosted glass effects** (background blurs but text stays sharp).
* Needs a **transparent background** to show effect.

<br>

## 📌 <mark>Available CSS Filters</mark>

* **`blur(px)`** → Gaussian blur (`10px` etc).
* **`brightness(%)` / decimal** → adjust brightness (`0%` = black, `100%` = normal, `>100%` = brighter).
* **`contrast(%)`** → adjusts contrast (`0%` = gray, `100%` = normal, `>100%` = more contrast).
* **`grayscale(%)`** → desaturates (`0%` = full color, `100%` = black & white).
* **`invert(%)`** → inverts colors (`100%` = fully inverted).
* **`opacity(%)`** → transparency (`0%` = invisible, `100%` = normal).
* **`saturate(%)`** → controls color intensity (`0%` = grayscale, `>100%` = super vivid).
* **`sepia(%)`** → adds warm brown tones (like old photos).
* **`hue-rotate(angle)`** → rotates colors on the hue wheel (e.g., `120deg`).
* **`drop-shadow(x y blur color)`** → shadow that follows the **shape** of the element (unlike `box-shadow`, no inset/spread).
* **`url(#filter-id)`** → apply an external **SVG filter**.

<details>
  <summary>Code</summary>

```html
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS Filters Demo</title>
    <style>
      body {
        font-family: sans-serif;
        background: url("https://picsum.photos/1200/800?blur=1") no-repeat
          center/cover;
        padding: 20px;
        color: #fff;
      }

      h2 {
        margin-top: 40px;
        color: yellow;
      }

      .demo {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
      }

      .box {
        width: 200px;
        height: 150px;
        background: url("https://picsum.photos/400/300") no-repeat center/cover;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-weight: bold;
        text-align: center;
        color: white;
        text-align: center;
      }

      /* Filters */
      .blur {
        filter: blur(5px);
      }
      .brightness {
        filter: brightness(50%);
      }
      .contrast {
        filter: contrast(200%);
      }
      .grayscale {
        filter: grayscale(100%);
      }
      .invert {
        filter: invert(100%);
      }
      .opacity {
        filter: opacity(50%);
      }
      .saturate {
        filter: saturate(200%);
      }
      .sepia {
        filter: sepia(100%);
      }
      .hue {
        filter: hue-rotate(120deg);
      }
      .drop {
        filter: drop-shadow(10px 10px 10px red);
      }

      /* Backdrop-filter example */
      .frosted {
        width: 300px;
        height: 150px;
        background: rgba(255, 255, 255, 0.2);
        backdrop-filter: blur(10px) brightness(80%);
        -webkit-backdrop-filter: blur(10px) brightness(80%);
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.2em;
        border-radius: 15px;
        border: 2px solid rgba(255, 255, 255, 0.3);
      }
    </style>
  </head>
  <body>
    <h1>🎨 CSS Filters Examples</h1>

    <h2>Filter on Elements</h2>
    <div class="demo">
      <div class="box blur">blur(5px)</div>
      <div class="box brightness">brightness(50%)</div>
      <div class="box contrast">contrast(200%)</div>
      <div class="box grayscale">grayscale(100%)</div>
      <div class="box invert">invert(100%)</div>
      <div class="box opacity">opacity(50%)</div>
      <div class="box saturate">saturate(200%)</div>
      <div class="box sepia">sepia(100%)</div>
      <div class="box hue">hue-rotate(120deg)</div>
      <div class="box drop">drop-shadow</div>
    </div>

    <h2>Backdrop Filter (Frosted Glass Effect)</h2>
    <div class="box frosted">✨ I blur the background, not the text!</div>
  </body>
</html>
```
</details>
  <img width="1129" height="708" alt="image" src="https://github.com/user-attachments/assets/4d78b175-531b-48c5-9a8b-b7521fca3a75" />


<br>

## 💡 Key Differences

* **`filter`** = applies to the element itself (text, image, etc).
* **`backdrop-filter`** = applies **only to the background behind** the element, not the element’s content.

<br>

👉 Example use case:

* `filter: blur(5px);` → blurs an image **and its text**.
* `backdrop-filter: blur(5px);` → blurs **only the background image**, while the **text stays sharp**.

