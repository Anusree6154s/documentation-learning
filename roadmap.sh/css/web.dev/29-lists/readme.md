
## 📋 CSS Lists 

### 1. Types of Lists

* **Unordered List (`<ul>`)** → Bullets (`•`) by default.
* **Ordered List (`<ol>`)** → Numbers (`1, 2, 3…`) by default.
* **Description List (`<dl>`)** → Uses `<dt>` (term) + `<dd>` (description).

<br>

### 2. Default behavior

* `<li>` has `display: list-item;` → automatically generates a `::marker`.

<br>

### 3. List Style Properties

* **`list-style-position`**

  * `outside` (default): bullet outside content box.
  * `inside`: bullet inside content box.

* **`list-style-image`**

  * Replace bullet with an image (e.g., `url(icon.png)`).
  * Limited control over size/position → better with `::marker`.

* **`list-style-type`**

  * Change bullet style: `disc`, `circle`, `square`, `decimal`, `lower-roman`, emoji, etc.

* **`list-style` shorthand**

  * Combine all:

    ```css
    list-style: square inside;
    list-style: url("icon.png") outside;
    list-style: none; /* remove bullets */
    ```


<br>

### 4. <mark>`::marker` pseudo-element</mark>

* Represents the **bullet/number** box of a list item.
* You can style it directly (instead of whole `<li>`).
* Supported properties:

  * `color`, `font-*`, `content`, `white-space`, `unicode-bidi`, plus animations/transitions.
* Example:

  ```css
  li::marker {
    content: "🥑 "; /* custom bullet */
    color: green;
    font-size: 1.2em;
  }
  ```

<br>

### 5.<mark> Marker Box</mark>

* The **container** that holds the bullet/number.
* Positioned before list item text.
* `::marker` gives you access to style this box.

<br>

### 6. `display: list-item`

* You can turn *any element* into a list item with:

  ```css
  h2 {
    display: list-item;
  }
  h2::marker {
    content: "★ ";
    color: gold;
  }
  ```
* ⚠️ Use semantic `<li>` for actual lists (accessibility).

<br>

✅ **In short:**
CSS lists are built with `<ul>`, `<ol>`, or `<dl>`.
You can style bullets using `list-style-*` properties, or use `::marker` for precise control.
And while `display: list-item` can fake a list, always use real `<li>` when it’s semantically a list.

## Examples
<details>
  <summary>Code</summary>

  ```html
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS List Examples</title>
    <style>
      /* 2. list-style-position */
      .outside {
        list-style-position: outside;
      }
      .inside {
        list-style-position: inside;
      }

      /* 3. list-style-image */
      .fruits {
        list-style-image: url("https://via.placeholder.com/15/ff0000"); /* tiny red square */
      }

      /* 4. list-style-type */
      .square {
        list-style-type: square;
      }
      .roman {
        list-style-type: lower-roman;
      }
      .emoji {
        list-style-type: "🍕 ";
      }

      /* 5. list-style shorthand */
      .shorthand {
        list-style: lower-roman inside;
      }

      /* 6. ::marker pseudo-element */
      .marker::marker {
        content: "🥑 ";
        color: green;
        font-size: 1.2em;
      }

      /* 7. display: list-item */
      .fake-list {
        display: list-item;
        list-style-position: outside;
        margin-inline-start: 1.25em;
      }
      .fake-list::marker {
        content: "★ ";
        color: gold;
      }
    </style>
  </head>
  <body>
    <h1>CSS Lists Examples</h1>

    <!-- 1. Types of Lists -->
    <h2>1. Types of Lists</h2>
    <p><b>Unordered List</b></p>
    <ul>
      <li>Milk</li>
      <li>Bread</li>
      <li>Eggs</li>
    </ul>

    <p><b>Ordered List</b></p>
    <ol>
      <li>Wake up</li>
      <li>Brush teeth</li>
      <li>Go to work</li>
    </ol>

    <p><b>Description List</b></p>
    <dl>
      <dt>HTML</dt>
      <dd>Structure of the web</dd>
      <dt>CSS</dt>
      <dd>Style for the web</dd>
    </dl>

    <!-- 2. list-style-position -->
    <h2>2. list-style-position</h2>
    <ul class="outside">
      <li>Outside bullet (default)</li>
    </ul>
    <ul class="inside">
      <li>Inside bullet</li>
    </ul>

    <!-- 3. list-style-image -->
    <h2>3. list-style-image</h2>
    <ul class="fruits">
      <li>Apple</li>
      <li>Banana</li>
      <li>Cherry</li>
    </ul>

    <!-- 4. list-style-type -->
    <h2>4. list-style-type</h2>
    <ul class="square">
      <li>Square bullet</li>
      <li>Another square</li>
    </ul>
    <ul class="roman">
      <li>Roman numeral</li>
      <li>Another roman numeral</li>
    </ul>
    <ul class="emoji">
      <li>Custom emoji bullet</li>
      <li>Another emoji bullet</li>
    </ul>

    <!-- 5. list-style shorthand -->
    <h2>5. list-style shorthand</h2>
    <ul class="shorthand">
      <li>Custom shorthand style</li>
      <li>Second shorthand item</li>
    </ul>

    <!-- 6. ::marker pseudo-element -->
    <h2>6. ::marker pseudo-element</h2>
    <ul>
      <li class="marker">Avocado</li>
      <li class="marker">Blueberry</li>
      <li class="marker">Carrot</li>
    </ul>

    <!-- 7. display: list-item -->
    <h2>7. display: list-item</h2>
    <h3 class="fake-list">This is styled like a list item</h3>
  </body>
</html>

```
</details>

<img width="280" height="674" alt="image" src="https://github.com/user-attachments/assets/8ece63ea-6fa9-4d1f-8921-cefd9ac77aa7" />
<img width="287" height="536" alt="image" src="https://github.com/user-attachments/assets/c064f6d0-dbbd-4f37-9831-9276b71552a2" />

