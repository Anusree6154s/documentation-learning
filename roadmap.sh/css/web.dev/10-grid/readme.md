
##  **Grid**

* `display: grid` turns an element into a grid container.
* Grid = rows + columns.
* Children = grid items → auto-placed or manually placed.
* Grid is **2D** (rows + columns) unlike flexbox (1D).


<br>

###  **Terminology**

* **Grid lines** → vertical & horizontal dividers, numbered.
* **Grid tracks** → space between 2 grid lines (rows/columns).
* **Grid cell** → smallest unit (like a table cell).
* **Grid area** → multiple cells combined.
* **Gaps** → spacing between tracks (set with `gap`).
* **Grid container** → parent with `display: grid`.
* **Grid item** → direct child of the container.

<img width="685" height="442" alt="image" src="https://github.com/user-attachments/assets/da37baf5-8887-4f78-94d3-800ce22f0043" />
<br>

###  **Creating Rows & Columns**

```css
.container {
  display: grid;
  grid-template-columns: 5em 100px 30%;
  grid-template-rows: 200px auto;
  gap: 10px;
}
```

* Units: px, em, %, `auto` (size by content).

<br>


###  **Track Sizing Keywords**

* `min-content` → as small as possible.
* `max-content` → as wide as content needs.
* `fit-content(x)` → max up to `x`, shrink if smaller.



###  **Special Units & Functions**

* **`fr` unit** → flexible share of leftover space.

  ```css
  grid-template-columns: 1fr 2fr 1fr;
  ```
* **`minmax(min, max)`** → control growth range.
* **`repeat(n, …)`** → shorthand for repeating patterns.
* **`auto-fill` / `auto-fit`** → auto-create as many columns as fit.

<br>


###  <mark> **Auto-placement**</mark>

* Default: items fill left → right, top → bottom.
* `grid-auto-flow: column` → fill down columns instead.
  * row: <img width="281" height="182" alt="image" src="https://github.com/user-attachments/assets/3db29c0d-9948-466b-99eb-310bbc95bb1a" />
  * column: <img width="281" height="190" alt="image" src="https://github.com/user-attachments/assets/15bd902e-2cbd-42f0-b7c1-4b45c36cec5c" />
* `span` → make item span multiple tracks.
* `grid-auto-flow: dense` → backfill empty gaps.
  * column normal: <img width="311" height="197" alt="image" src="https://github.com/user-attachments/assets/25d8c1b6-75f8-4773-a798-37b3155f7df2" />
  * column with dense: <img width="297" height="202" alt="image" src="https://github.com/user-attachments/assets/4fbac730-1bb5-4285-8388-3eec8bda6c69" />
  

<br>



### <mark> **Placing Items**</mark>

* Line-based placement:

  ```css
  .item {
    grid-column: 1 / 4;
    grid-row: 2 / 4;
  }
  ```
* `-1` = last line of explicit grid.
* Implicit tracks created automatically → can size with:

  ```css
  grid-auto-rows: minmax(10em, auto);
  ```
<br>



### <mark> **Named Lines & Areas** </mark>

* **Named lines**:

  ```css
  grid-template-columns:
    [main-start aside-start] 1fr
    [aside-end content-start] 2fr
    [content-end main-end];
  ```
* **Named areas** (`grid-template-areas`):

  ```css
  grid-template-areas:
    "header header header"
    "sidebar content content"
    "sidebar footer footer";
  ```
<details>
  <summary>More explanation</summary>

## ✅ Example: Layout with Named Lines & Areas

```html
<div class="container">
  <header>Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Content</main>
  <footer>Footer</footer>
</div>
```

```css
.container {
  display: grid;
  grid-template-columns:
    [main-start aside-start] 1fr
    [aside-end content-start] 2fr
    [content-end main-end];   /* Named lines */
    
  grid-template-rows: auto 1fr auto;

  /* Named areas */
  grid-template-areas:
    "header  header   header"
    "sidebar content  content"
    "sidebar footer   footer";

  gap: 10px;
  height: 100vh;
  border: 3px solid black;
}

header {
  grid-area: header;
  background: lightblue;
}

.sidebar {
  grid-area: sidebar;
  background: lightcoral;
}

.content {
  grid-area: content;
  background: lightgreen;
}

footer {
  grid-area: footer;
  background: peachpuff;
}
```



### 🔍 What’s happening here:

* **Named lines**:

  ```css
  [main-start aside-start] 1fr
  [aside-end content-start] 2fr
  [content-end main-end];
  ```

  * Gives the grid lines meaningful names instead of numbers.
  * Example: the sidebar could be placed with

    ```css
    .sidebar { grid-column: aside-start / aside-end; }
    ```

* **Named areas**:

  ```css
  grid-template-areas:
    "header  header   header"
    "sidebar content  content"
    "sidebar footer   footer";
  ```

  * Lets you map elements to **visual areas**.
  * Each child element uses `grid-area: name;` to slot into the right place.
</details>

###  **Shortcuts**

* `grid-template` → combines rows, cols, and areas.
* `grid` → combines template + auto rows/cols/flow.

<br>


### <mark> **Subgrid** </mark>

* Nested grids can align with parent tracks:

  ```css
  grid-template-columns: subgrid;
  grid-template-rows: subgrid;
  ```

  <img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/35c61196-af03-46e2-a1a5-b09b5b8c3915" />

* Without subgrid, every nested grid creates its own track sizing. That means the inner grid’s columns/rows won’t line up with the parent grid unless you manually duplicate the track definitions.
```css
/*without subgrid*/
.container {
  display: grid;
  grid-template-columns: 150px 1fr 150px;
  grid-template-rows: auto 1fr auto;
  gap: 10px;
}

.content {
  display: grid;
  grid-template-columns: 150px 1fr 150px; /* ❌ must duplicate parent */
  gap: 10px; /* ❌ must duplicate parent */
}

```

<br>


###  **Alignment**

* `justify-` → inline axis (left–right in LTR).
* `align-` → block axis (top–bottom).
* Container:

  * `justify-content`, `align-content`.
  * `justify-items`, `align-items`.
* Items:

  * `justify-self`, `align-self`.


<br>

✅ **In short**:
CSS Grid = the most powerful **2D layout system in CSS** with control over rows + columns, flexible sizing (`fr`, `minmax`), auto-placement, named areas, subgrid, and alignment.

