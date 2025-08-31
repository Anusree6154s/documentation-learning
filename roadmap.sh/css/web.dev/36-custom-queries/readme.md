

## 🔹 Container Queries in CSS

### 1. Difference from Media Queries

* **Media queries** → adjust based on **viewport/device size**.
* **Container queries** → adjust based on the **size/state of ancestor container(s)**.

<br>

### 2. Use Case

* Components (like a **newsletter sign-up form**) can adapt layout depending on the **container** they’re placed in, not just the screen size.

<br>

### 3. Setting up a Container Query

Two steps:

1. **Define a container** with `container-type`.
2. **Write container query styles** for its children.

<br>

### 4. Defining a Container

* `container-type: inline-size;` → query container’s **inline axis (width)**.
* `container-type: size;` → query both **inline + block axes (width + height)**.
* Requires explicit dimensions if children don’t size it automatically.

```css
.my-container {
  container-type: inline-size;
}
```

<br>

### 5. Container Query Conditions

* Size features: `width`, `height`, `inline-size`, `block-size`, `aspect-ratio`, `orientation`.
* Operators: `<, >, <=, >=, =`.

Examples:

```css
@container (min-width: 300px) { ... }
@container (inline-size > 40em) and (orientation: landscape) { ... }
@container (10em <= width <= 500px) { ... }
```

<br>

### 6. Naming Containers

* Use `container-name` to target a **specific ancestor container**.

```css
.sidebar {
  container-name: main-sidebar;
  container-type: inline-size;
}

@container main-sidebar (inline-size > 20em) {
  .button-group { display: flex; }
}
```

* Shorthand: `container: name / type;`

<br>

### 7. Container Query Units

* Units relative to container size (`cqi`, `cqb`, `cqw`, `cqh`).
* Example: `1cqi = 1% of container’s inline size`.

```css
button {
  padding: 2cqi 5cqi; /* adapts to container size */
}
```

<br>

### 8. Nesting Container Queries

* Can nest inside selectors or other at-rules.

```css
.my-element {
  display: grid;

  @container my-container (min-inline-size: 22em) {
    grid-template-columns: 1fr 1fr;
  }
}
```




<br>

✅ **In summary:**

* Media queries = **viewport-based**.
* Container queries = **parent-container-based**.
* Define container → apply queries → optional naming + container-relative units.

  ## Examples

  <details>
    <summary>Code</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Container Queries Examples</title>
        <style>
          body {
            font-family: sans-serif;
            display: flex;
            gap: 2rem;
            flex-wrap: wrap;
            padding: 2rem;
          }
    
          /* 1. Basic container */
          .basic-container {
            container-type: inline-size;
            border: 2px solid steelblue;
            padding: 1rem;
            width: 350px;
          }
    
          .card {
            background: lightsteelblue;
            padding: 1rem;
            text-align: center;
          }
    
          @container (min-width: 300px) {
            .card {
              background: cornflowerblue;
              color: white;
              font-size: 1.2rem;
            }
          }
    
          /* 2. Named container */
          .sidebar {
            container: main-sidebar / inline-size;
            border: 2px dashed seagreen;
            padding: 1rem;
            width: 280px;
          }
    
          .button-group button {
            display: block;
            margin: 0.5rem 0;
            padding: 0.5rem;
            width: 100%;
          }
    
          @container main-sidebar (min-width: 200px) {
            .button-group {
              display: flex;
              gap: 0.5rem;
            }
    
            .button-group button {
              flex: 1;
            }
          }
    
          /* 3. Container units */
          .unit-container {
            container: button-container / inline-size;
            border: 2px solid darkorange;
            padding: 1rem;
            width: 200px;
          }
    
          .unit-container button {
            padding: 2cqi 5cqi; /* relative to container width */
            background: orange;
            border: none;
            border-radius: 6px;
            color: white;
          }
    
          /* 4. Nesting queries */
          .nested-container {
            container: nested / inline-size;
            border: 2px solid darkred;
            padding: 1rem;
            width: 350px;
          }
    
          .nested-card {
            background: pink;
            padding: 1rem;
            text-align: center;
          }
    
          @container nested (min-width: 240px) {
            .nested-card {
              background: crimson;
              color: white;
            }
    
            @container nested (min-width: 300px) {
              .nested-card {
                background: purple;
              }
            }
          }
        </style>
      </head>
      <body>
        <!-- 1. Basic -->
        <div class="basic-container">
          <div class="card">Basic Container Query</div>
        </div>
    
        <!-- 2. Named Container -->
        <div class="sidebar">
          <div class="button-group">
            <button>One</button>
            <button>Two</button>
            <button>Three</button>
          </div>
        </div>
    
        <!-- 3. Container Units -->
        <div class="unit-container">
          <button>Container Unit Button</button>
        </div>
    
        <!-- 4. Nested Queries -->
        <div class="nested-container">
          <div class="nested-card">Nested Container Query</div>
        </div>
      </body>
    </html>

    ```
  </details>

https://github.com/user-attachments/assets/90e3508b-a0a4-4dd3-87e1-3ad3f37ab93b
