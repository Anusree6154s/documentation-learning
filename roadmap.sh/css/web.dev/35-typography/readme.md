
## **Text & Typography (CSS)**

### General

* Text is a core building block of the web.
* HTML provides default styles, but CSS enhances readability and design.
* Small changes (font, spacing, alignment) can greatly improve UX.

<br>

### <mark> **@font-face Rule**</mark>

* Lets you import and use custom fonts (local or remote).
* Syntax:

  ```css
  @font-face {
    font-family: "CustomFont";
    src: local("CustomFont"), url("customfont.woff2") format("woff2");
  }
  ```
* Key descriptors:

  * `font-family`: name of the font.
  * `src`: font source (local() or url()).
  * `font-weight`, `font-style`, `font-stretch`: style variations.
  * `unicode-range`: limit which characters the font applies to.
  * `font-display`: controls rendering while loading.
* MIME types:

  * `.ttf` → `font/ttf`
  * `.otf` → `font/otf`
  * `.woff` → `font/woff`
  * `.woff2` → `font/woff2`

<br>

### **Font Properties**

* **font-family**: sets typeface; use fallback fonts (e.g., `"Helvetica", sans-serif`).
* **font-style**: `normal`, `italic` (cursive variant), `oblique` (slanted).
* **font-weight**:

  * `normal` (400), `bold` (700), `lighter`, `bolder`.
  * Numeric: 100–900.
  * Custom weights require variable fonts.
* **font-size**:

  * Keywords: `small`, `medium`, `large`.
  * Units: px, em (relative to parent), rem (relative to root).
* **line-height**: controls vertical spacing between lines (use numbers for consistency).

<br>

### **Spacing**

* **letter-spacing**: adjusts space between characters.
* **word-spacing**: adjusts space between words.
* **text-indent**: indents the first line of a block.

<br>

### **Text Decoration**

* **text-decoration**: add underline, overline, line-through.
* Sub-properties:

  * `text-decoration-line`
  * `text-decoration-color`
  * `text-decoration-style` (solid, dashed, wavy, etc.)
  * <mark>`text-decoration-thickness`</mark>
* **text-shadow**: adds shadows (x-offset, y-offset, blur-radius, color).

<br>

### **Text Transformations**

* **text-transform**: `uppercase`, `lowercase`, `capitalize`.
* **text-overflow**: `clip` or `ellipsis (…)`.
* **white-space**: controls handling of spaces and line breaks (`normal`, `pre`, `nowrap`).
* **word-break**: `normal`, `break-all`, `keep-all`.
* **overflow-wrap**: `normal`, `break-word`, `anywhere`.
* **text-align**: `left`, `right`, `center`, `justify`, `start`, `end`.
* **text-wrap**: `wrap`, `nowrap`, `balance`, `stable`.

<br>

### **Text Direction & Flow**

* **direction**: `ltr` (default) or `rtl` (for languages like Arabic/Hebrew).
* **writing-mode**: text flow (`horizontal-tb`, `vertical-lr`, `vertical-rl`).
* **text-orientation**: `mixed`, `upright` (for vertical writing).

<br>

### <mark>**Advanced Typography**</mark>

* **Variable Fonts**: multiple weights/styles in one font file (e.g., Roboto Flex).
* **font-variant**: shorthand for specialized variants (small-caps, ligatures, numeric styles).

<br>

### **Pseudo-elements**

* `::first-letter`: style the first letter of a block.
* `::first-line`: style the first line of text.
* `::selection`: style selected text (limited properties).

<br>

✅ **Summary**:

* `@font-face` = defines/imports a font.
* `font-family` = applies fonts to elements.
* Core properties = size, weight, style, spacing, alignment.
* Extra control via text-transform, decoration, shadows, pseudo-elements.
* Advanced typography via variable fonts & font-variant.

  ## Examples

  <details>
    <summary>Code</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <title>CSS Text & Typography Examples</title>
        <style>
          @font-face {
            font-family: "CustomFont";
            src: url("customfont.woff2") format("woff2");
            font-weight: 400;
            font-style: normal;
          }
          body {
            font-family: Arial, sans-serif;
            padding: 20px;
            line-height: 1.5;
          }
          section {
            margin-bottom: 2em;
            border: 2px gray dashed;
            padding: 10px;
            border-radius: 10px;
          }
          h2 {
            margin-top: 1em;
          }
          .font-family {
            font-family: "Courier New", monospace;
          }
          .font-style-italic {
            font-style: italic;
          }
          .font-style-oblique {
            font-style: oblique;
          }
          .font-weight {
            font-weight: 700;
          }
          .font-size {
            font-size: 24px;
          }
          .line-height {
            line-height: 2;
            background: #f0f0f0;
          }
          .letter-spacing {
            letter-spacing: 5px;
          }
          .word-spacing {
            word-spacing: 20px;
          }
          .text-indent {
            text-indent: 50px;
          }
          .underline {
            text-decoration: underline;
          }
          .overline {
            text-decoration: overline;
          }
          .line-through {
            text-decoration: line-through;
          }
          .decoration-style {
            text-decoration: underline wavy red 2px;
          }
          .text-shadow {
            text-shadow: 2px 2px 5px gray;
          }
          .uppercase {
            text-transform: uppercase;
          }
          .lowercase {
            text-transform: lowercase;
          }
          .capitalize {
            text-transform: capitalize;
          }
          .overflow {
            width: 150px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            border: 1px solid #ccc;
          }
          .nowrap {
            white-space: nowrap;
          }
          .pre {
            white-space: pre;
          }
          .break-all {
            word-break: break-all;
          }
          .overflow-wrap {
            overflow-wrap: break-word;
          }
          .align-center {
            text-align: center;
          }
          .align-justify {
            text-align: justify;
          }
          .rtl {
            direction: rtl;
          }
          .vertical {
            writing-mode: vertical-rl;
          }
          .upright {
            writing-mode: vertical-rl;
            text-orientation: upright;
          }
          .small-caps {
            font-variant: small-caps;
          }
          .first-letter::first-letter {
            font-size: 2em;
            color: red;
          }
          .first-line::first-line {
            font-weight: bold;
          }
          .selection::selection {
            background: yellow;
            color: black;
          }
        </style>
      </head>
      <body>
        <h1>CSS Text & Typography Examples</h1>
        <section>
          <h2>@font-face</h2>
          <p style="font-family: CustomFont">This uses a custom font.</p>
        </section>
        <section>
          <h2>Font Properties</h2>
          <p class="font-family">Font Family Example</p>
          <p class="font-style-italic">Italic</p>
          <p class="font-style-oblique">Oblique</p>
          <p class="font-weight">Bold Weight</p>
          <p class="font-size">Large Font Size</p>
          <p class="line-height">Line height makes text more spaced vertically.</p>
        </section>
        <section>
          <h2>Spacing</h2>
          <p class="letter-spacing">Letter Spacing</p>
          <p class="word-spacing">Word Spacing Example</p>
          <p class="text-indent">Indented first line.</p>
        </section>
        <section>
          <h2>Decoration</h2>
          <p class="underline">Underline</p>
          <p class="overline">Overline</p>
          <p class="line-through">Line Through</p>
          <p class="decoration-style">Wavy Red Underline</p>
          <p class="text-shadow">Text Shadow Effect</p>
        </section>
        <section>
          <h2>Transform & Overflow</h2>
          <p class="uppercase">uppercase</p>
          <p class="lowercase">LOWERCASE</p>
          <p class="capitalize">capitalize each word</p>
          <p class="overflow">This text is too long and will show ellipsis.</p>
          <p class="nowrap">This text will not wrap onto a new line.</p>
          <p class="pre">Preserved spaces and new lines</p>
          <p class="break-all">averylongwordwithoutspaceswillbreak</p>
          <p class="overflow-wrap">averyveryverylongwordwillbreakhere</p>
          <p class="align-center">Centered Text</p>
          <p class="align-justify">
            Justified text fills the whole width of the box evenly.
          </p>
        </section>
        <section>
          <h2>Direction & Flow</h2>
          <p class="rtl">مرحبا بالعالم</p>
          <p class="vertical">Vertical writing mode</p>
          <p class="upright">Upright characters</p>
        </section>
        <section>
          <h2>Advanced Typography</h2>
          <p class="small-caps">Small caps style</p>
        </section>
        <section>
          <h2>Pseudo-elements</h2>
          <p class="first-letter">This paragraph has a styled first letter.</p>
          <p class="first-line">
            This paragraph has a bold first line to show styling.
          </p>
          <p class="selection">Select this text to see selection styling.</p>
        </section>
      </body>
    </html>

    ```
  </details>
  <img width="300" height="211" alt="image" src="https://github.com/user-attachments/assets/dc4d4594-4234-45bd-8784-d2809dcd6eeb" />
  <img width="300" height="531" alt="image" src="https://github.com/user-attachments/assets/39e37b3b-f372-459a-958c-5640ae1fa351" />
  <img width="300" height="575" alt="image" src="https://github.com/user-attachments/assets/6f37add5-1e02-4d23-983e-7237946aa8be" />
  <img width="300" height="521" alt="image" src="https://github.com/user-attachments/assets/a7d52141-e6c5-41d6-a6f3-25317bcb0b2f" />
  <img width="300" height="614" alt="image" src="https://github.com/user-attachments/assets/27a6a391-82d8-43a7-9b7d-2392ad940db8" />
  <img width="300" height="444" alt="image" src="https://github.com/user-attachments/assets/44a5b185-db19-41bd-9730-1f43a9063807" />






