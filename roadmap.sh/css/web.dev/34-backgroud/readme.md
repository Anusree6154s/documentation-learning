
## 🎨 CSS Backgrounds 

### 1. **Background Layer**

* Background is painted **behind the content & padding** of a box.
* Does **not overlap with borders** by default.

<br>

### 2. **Background Color**

* Property: `background-color`
* Default: `transparent` (shows parent’s background).
* Example:

  ```css
  div {
    background-color: lightblue;
  }
  ```

<br>

### 3. **Background Images**

* Property: `background-image`
* Accepts:

  * `url("image.png")`
  * `linear-gradient(...)` / `radial-gradient(...)`
* Example:

  ```css
  div {
    background-image: url("bg.png");
  }
  ```

<br>

### 4. **Repeating Backgrounds**

* Property: `background-repeat`
* Values:

  * `repeat` (default, x & y)
  * `repeat-x`
  * `repeat-y`
  * `no-repeat`
  * `round` (stretches / compresses to fit)
  * `space` (spaces evenly with gaps)
* Example:

  ```css
  div {
    background-repeat: repeat-x;
  }
  ```

<br>

### 5. **Background Position**

* Property: `background-position`
* Sets X (horizontal) & Y (vertical) offsets.
* Can use **keywords**, **percentages**, or **lengths**.
* Examples:

  ```css
  background-position: top left;
  background-position: 50% 20%;
  background-position: bottom 20% right 30%;
  ```

<br>

### 6. **Background Size**

* Property: `background-size`
* Values:

  * `auto` (default, natural size)
  * `cover` (fills box, may crop)
  * `contain` (fits inside box, may leave gaps)
* Example:

  ```css
  background-size: cover;
  ```

<br>

### 7. <mark>**Background Attachment**</mark>

* Property: `background-attachment`
* Values:

  * `scroll` (default, moves with page)
  * `fixed` (stays relative to viewport)
  * `local` (moves with element’s content)
* Example:

  ```css
  background-attachment: fixed;
  ```

<br>

### 8. <mark>**Background Origin**</mark>

* Property: `background-origin`
* Defines where the background starts painting:

  * `border-box`
  * `padding-box` (default)
  * `content-box`
* Example:

  ```css
  background-origin: content-box;
  ```

<br>

### 9. <mark>**Background Clip**</mark>

* Property: `background-clip`
* Defines where the background is **visible**:

  * `border-box`
  * `padding-box`
  * `content-box`
  * `text` (clips background to text shape → needs transparent text + `-webkit-background-clip` in some browsers)
* Example:

  ```css
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  ```

<br>

### 10. <mark>**Multiple Backgrounds**</mark>

* You can **stack multiple backgrounds** with commas.
* First one = topmost (closest to user).
* Example:

  ```css
  div {
    background-image: 
      url("top.png"),
      url("middle.png"),
      linear-gradient(blue, lightblue);
  }
  ```

<br>

### 11. **Background Shorthand**

* Combines multiple background properties into one.
* Syntax:

  ```css
  background: 
    <image> 
    <position> / <size> 
    <repeat> 
    <attachment> 
    <origin> 
    <clip> 
    <color>;
  ```
* Example:

  ```css
  background: url("bg.png") center/cover no-repeat fixed padding-box content-box lightgray;
  ```

## Examples

<details>
  <summary>Code</summary>

  ```html
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Backgrounds Demo</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        margin: 20px;
        background: #f0f0f0;
      }
      h2 {
        margin-top: 50px;
        color: #333;
      }
      .demo {
        width: 300px;
        height: 150px;
        border: 2px solid #333;
        margin: 15px 0;
        padding: 10px;
        color: white;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      /* 1. Background Color */
      .bg-color {
        background-color: lightseagreen;
      }

      /* 2. Background Image */
      .bg-image {
        background-image: url("https://picsum.photos/200");
      }

      /* 3. Background Repeat */
      .bg-repeat {
        background-image: url("https://www.w3.org/html/logo/downloads/HTML5_Logo_32.png");
        background-repeat: repeat-x;
      }

      /* 4. Background Position */
      .bg-position {
        background-image: url("https://www.w3.org/html/logo/downloads/HTML5_Logo_32.png");
        background-repeat: no-repeat;
        background-position: bottom right;
      }

      /* 5. Background Size */
      .bg-size {
        background-image: url("https://picsum.photos/200");
        background-size: cover;
        background-repeat: no-repeat;
      }

      /* 6. Background Attachment */
      .bg-attachment {
        background-image: url("https://picsum.photos/600/400");
        background-attachment: fixed;
        background-size: cover;
        background-repeat: no-repeat;
      }

      /* 7. Background Origin */
      .bg-origin {
        background-image: url("https://picsum.photos/200");
        background-repeat: no-repeat;
        background-origin: content-box;
        padding: 30px;
      }

      /* 8. Background Clip */
      .bg-clip {
        background: linear-gradient(to right, red, blue);
        -webkit-background-clip: text;
        color: transparent;
        font-size: 28px;
        font-weight: bold;
        justify-content: flex-start;
      }

      /* 9. Multiple Backgrounds */
      .bg-multiple {
        background-image: url("https://www.w3.org/html/logo/downloads/HTML5_Logo_32.png"),
          url("https://picsum.photos/200"), linear-gradient(45deg, orange, pink);
        background-repeat: no-repeat, no-repeat, no-repeat;
        background-position: left top, right bottom, center;
        background-size: auto, 100px, cover;
      }

      /* 10. Shorthand */
      .bg-shorthand {
        background: url("https://picsum.photos/300") center/cover no-repeat
          fixed border-box content-box;
      }
    </style>
  </head>
  <body>
    <h1>CSS Backgrounds Demo</h1>

    <h2>1. Background Color</h2>
    <div class="demo bg-color">background-color</div>

    <h2>2. Background Image</h2>
    <div class="demo bg-image">background-image</div>

    <h2>3. Background Repeat</h2>
    <div class="demo bg-repeat">background-repeat</div>

    <h2>4. Background Position</h2>
    <div class="demo bg-position">background-position</div>

    <h2>5. Background Size</h2>
    <div class="demo bg-size">background-size</div>

    <h2>6. Background Attachment (scroll page)</h2>
    <div class="demo bg-attachment">background-attachment</div>
    <p style="height: 200px">Scroll down to see fixed background</p>

    <h2>7. Background Origin</h2>
    <div class="demo bg-origin">background-origin</div>

    <h2>8. Background Clip (text)</h2>
    <div class="demo bg-clip">background-clip: text</div>

    <h2>9. Multiple Backgrounds</h2>
    <div class="demo bg-multiple">multiple backgrounds</div>

    <h2>10. Background Shorthand</h2>
    <div class="demo bg-shorthand">shorthand</div>
  </body>
</html>

```
</details>


<img width="394" height="591" alt="image" src="https://github.com/user-attachments/assets/1e5ed33d-4a2a-4d9f-ac4e-cf042948f382" />
<img width="256" height="583" alt="image" src="https://github.com/user-attachments/assets/21f2a6b8-c7a7-4456-b89b-1230d78f07f4" />

https://github.com/user-attachments/assets/57cc3694-637e-49a6-ac25-37a2edbe0621

<img width="285" height="618" alt="image" src="https://github.com/user-attachments/assets/bdd084d5-afbd-4a24-877b-eb8154d3acfe" />
<img width="250" height="178" alt="image" src="https://github.com/user-attachments/assets/6652686c-58df-4bae-85ab-b42c523e3d46" />

