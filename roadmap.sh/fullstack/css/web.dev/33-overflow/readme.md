
## 🌊 CSS Overflow 

### 1. What is overflow?

* When content extends beyond its parent’s defined space.
* Options: **scroll, clip, ellipsis (for text), hidden**, etc.
* Important for responsive layouts & mobile screens.

<br>

### 2. Types of clipping

* **`text-overflow`** → Works on single-line text only.

  ```css
  p {
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
  }
  ```
* **`overflow` properties** → Work on block/box elements.

<br>

### 3. Overflow axes

* **`overflow-x`** → Controls horizontal overflow.
* **`overflow-y`** → Controls vertical overflow.
* <mark>**Logical alternatives**: `overflow-inline`, `overflow-block`.</mark>

<br>

### 4. Overflow shorthand

* `overflow: hidden scroll;` → first value = x-axis, second = y-axis.
* `overflow: auto;` → most common, scrollbars only if needed.

<br>

### 5. Overflow values

* **`visible`** (default) → content spills out, never hidden.
* **`hidden`** → content clipped, no scrollbars.
* **`scroll`** → always shows scrollbars, even if not needed.
* **`clip`** → like hidden, but forbids all scrolling (even JS).
* **`auto`** → scrollbars only when content overflows.

<br>

### 6. Accessibility & scrolling

* <mark>Scrollable areas should be **focusable** for keyboard users.</mark>

  ```html
  <div tabindex="0" role="region" aria-labelledby="desc">
    content
  </div>
  ```
* Style focus:

  ```css
  [role][aria-labelledby][tabindex]:focus {
    outline: .1em solid blue;
  }
  ```

<br>

### 7. Scrollbars in the box model

* Scrollbars take up space inside the **padding box**.
* <mark>Can cause **layout shift**.</mark>

<br>

### 8. Root vs. implicit scrollers

* **Root scroller** → usually `<html>`/`documentElement`.
  <details>
    <summary>Code</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Root Scroller Example</title>
        <style>
          body {
            margin: 0;
            height: 200vh; /* make page taller */
            background: linear-gradient(lightblue, lightgreen);
          }
        </style>
      </head>
      <body>
        <h2>Root Scroller (Default)</h2>
        <p>
          Scroll this page — you're scrolling the root scroller (`documentElement`).
        </p>
      </body>
    </html>

    ```
    
  </details>
  

https://github.com/user-attachments/assets/a660d37c-89a6-4f1f-bda6-791f65713254





* Can <mark>promote another element to root scroller (e.g., fixed overlay).</mark>

<details>
  <summary>Code</summary>

  ```html
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Promoted Root Scroller Example</title>
    <style>
      body {
        margin: 0;
        background: gray;
        height: 200vh; /* original body is tall, but won't scroll */
      }

      .overlay-root {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        overflow: auto; /* makes this the "root scroller" */
        background: white;
      }

      .content {
        height: 300vh;
        background: linear-gradient(lightcoral, lightseagreen);
      }
    </style>
  </head>
  <body>
    <div class="overlay-root">
      <h2>Promoted Root Scroller</h2>
      <p>This fixed overlay takes over as the root scroller.</p>
      <div class="content"></div>
    </div>
  </body>
</html>

```
</details>


https://github.com/user-attachments/assets/135e5004-af74-435c-b9b1-ddcf1c0cb86d


* Root scroller = has special behaviors (pull-to-refresh, bounce).


<br>

### 9. Styling scrollbars

* **`scrollbar-color`** → thumb & track color.
* **`scrollbar-width`** → can be `auto`, `thin`, or `none`.

<br>

### 10. Scroll behavior

* **`scroll-behavior`** → controls smooth scrolling.

  ```css
  @media (prefers-reduced-motion: no-preference) {
    .scroll-view { scroll-behavior: smooth; }
  }
  ```
* Respects user preferences (`prefers-reduced-motion`).

<br>

### 11. Overscroll behavior

* <mark>**`overscroll-behavior`** → prevents scroll chaining.</mark>
* Example: stop background page from scrolling when modal hits edge.

<br>

### 12. Scroll snapping

* **`scroll-snap-type`** → defines axis (`x`, `y`, `block`, `inline`, `both`) + strictness (`proximity`, `mandatory`).
* **`scroll-snap-align`** → where item aligns (`start`, `center`, `end`).
* **`scroll-padding`** → offset for fixed headers, etc.
* **`scroll-margin`** → space around snap elements.
* **`scroll-snap-stop: always`** → makes snapping stronger.

## Examples
<details>
  <summary>Code</summary>

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>CSS Overflow Demo</title>
      <style>
        body {
          font-family: Arial, sans-serif;
          margin: 20px;
        }
  
        /* 1. Text Overflow */
        .text-overflow {
          width: 200px;
          border: 1px solid #333;
          padding: 5px;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }
  
        /* 2. Overflow Hidden */
        .hidden-box {
          width: 200px;
          height: 80px;
          border: 1px solid red;
          overflow: hidden;
        }
  
        /* 3. Overflow Scroll */
        .scroll-box {
          width: 200px;
          height: 80px;
          border: 1px solid blue;
          overflow: scroll;
        }
  
        /* 4. Overflow Auto */
        .auto-box {
          width: 200px;
          height: 80px;
          border: 1px solid green;
          overflow: auto;
        }
  
        /* 5. Overscroll Behavior */
        .overscroll-box {
          width: 200px;
          height: 100px;
          border: 2px solid purple;
          overflow: auto;
          overscroll-behavior: contain;
        }
  
        /* 6. Scroll Snapping */
        .scroll-container {
          width: 250px;
          height: 150px;
          border: 2px solid black;
          overflow-x: auto;
          scroll-snap-type: x mandatory;
          display: flex;
        }
  
        .snap-item {
          flex: none;
          width: 250px;
          height: 150px;
          scroll-snap-align: start;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 20px;
          color: white;
        }
  
        .item1 {
          background: crimson;
        }
        .item2 {
          background: royalblue;
        }
        .item3 {
          background: seagreen;
        }
      </style>
    </head>
    <body>
      <h2>1. Text Overflow</h2>
      <div class="text-overflow">
        This is a very long sentence that will be clipped with ellipsis.
      </div>
  
      <h2>5. Overscroll Behavior (No Scroll Chaining)</h2>
      <div class="overscroll-box">
        Try scrolling here. Even if you reach the end, the page behind this box
        won’t scroll. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
        Proin volutpat metus in tristique malesuada.
      </div>
  
      <h2>2. Overflow Hidden</h2>
      <div class="hidden-box">
        This content is too tall for the box, but you won’t see the rest of it
        because it’s clipped. Extra hidden text...
      </div>
  
      <h2>3. Overflow Scroll</h2>
      <div class="scroll-box">
        Lots of content here. Keep scrolling down and sideways to read all of it.
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec non turpis
        vel lorem volutpat varius.
      </div>
  
      <h2>4. Overflow Auto</h2>
      <div class="auto-box">
        If this text overflows, scrollbars will appear. Otherwise, they won’t.
        Lorem ipsum dolor sit amet, consectetur adipiscing elit.
      </div>
  
      <h2>6. Scroll Snapping</h2>
      <div class="scroll-container">
        <div class="snap-item item1">Slide 1</div>
        <div class="snap-item item2">Slide 2</div>
        <div class="snap-item item3">Slide 3</div>
      </div>
    </body>
  </html>

```
</details>



https://github.com/user-attachments/assets/b5983ddc-362c-42aa-8660-18a36bc10d1f

