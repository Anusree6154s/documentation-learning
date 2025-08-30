# Sizing Units

## 🔢 Numbers

* **Unitless numbers** → used in opacity, line-height, rgb, filters, transform.

  * `line-height: 1.5;` → 150% of font size (good practice to keep unitless).
  * `opacity: 0.5;` → 50% opacity.
  * `scale(1.2)` → scales to 120%.
  * `rgb(50,50,50)` → grayscale.


## 📊 Percentages (%)

* Calculated relative to **something else** (depends on property):

  * `width: 50%` → relative to parent’s width.
  * `padding/margin: 50%` → relative to parent’s width (always, even vertical).
  * `transform: translateX(10%)` → relative to element’s own size.


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
  * <details>
     <summary><mark> Used in media queries to detect high-res displays</mark> (e.g. Retina).</summary>

       ## 1. **Resolution units**
    
       * `dpi` = dots per inch
       * `dpcm` = dots per centimeter
       * `dppx` = dots per CSS pixel (relative to 1px at 96dpi → so `1dppx = 96dpi`)
       
       They are most often used in **media queries** to check whether the display has a high pixel density.
       
       
       
       ## 2. **Why?**
       
       High-DPI displays (e.g. Retina, 4K phones) pack more device pixels into the same CSS pixel size. If you serve a normal-resolution image, it looks **blurry**.
       So you check resolution → then serve higher-res assets.
    
    
    
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
    
    
    
    ### Using `dpi`
    
    ```css
    @media (min-resolution: 192dpi) {
      .logo {
        background-image: url("logo@2x.png");
      }
    }
    ```
    
    * `192dpi` is equivalent to `2dppx` because `1dppx = 96dpi`.
    
    
    
    ### Using `dpcm`
    
    ```css
    @media (min-resolution: 75dpcm) {
      .logo {
        background-image: url("logo@2x.png");
      }
    }
    ```
    
    * `75dpcm` ≈ `192dpi`.
    
    
    
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
    <mark>You use `dpi`, `dpcm`, or `dppx` inside `@media` queries to detect when a device has a **high pixel density display** and swap in higher-resolution assets (images, icons, etc.) to keep them sharp.</mark>

  </details>




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
