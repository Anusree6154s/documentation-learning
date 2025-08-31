
## 📌 CSS Transitions 

### 🔹 1. What are transitions?

* By default, CSS state changes (hover, focus, open/close, etc.) happen instantly.
* **Transitions interpolate** between the start and end state → smooth animation.
* Improves UX by giving visual feedback and natural movement.

<br>




### 🔹 2. Transition Properties

* `transition-property`: which CSS property to animate.

  ```css
  transition-property: background-color;  
  transition-property: all; /* animates everything */
  ```
* `transition-duration`: how long the transition lasts (`s` or `ms`).

  ```css
  transition-duration: 300ms;
  ```
* `transition-timing-function`: controls acceleration/speed curve.

  * `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`, or custom `cubic-bezier`.
* `transition-delay`: when the transition starts (can be negative).

<br>

### 🔹 3. Shorthand

```css
.my-element {
  transition: transform 300ms ease-in-out 0s;
}
```

\= property + duration + easing + delay.

<br>

### 🔹 4. What can transition?

✅ Animatable: numeric or measurable values (colors, opacity, transform, size, shadow, filter).
❌ Not animatable: discrete changes (e.g., `font-family`, `display`).

<br>

### 🔹 5. Common Transitioned Properties

* **Transform** → scale, rotate, translate, skew. (GPU accelerated, smooth).
* **Colors** → `color`, `background-color`, `border-color`.
* **Shadows** → `box-shadow` for elevation/focus feedback.
* **Filters** → blur, brightness, contrast, grayscale.

<br>

### 🔹 6. Transition Triggers

* Pseudo-classes:

  * `:hover` → when mouse hovers.
  * `:focus` / `:focus-within` → focus state.
  * `:target` → when URL fragment matches element ID.
  * `:active` → while pressing/clicking.
* Class changes via JavaScript → transitions animate between styles.

<br>

### 🔹 7. Enter vs Exit Transitions

You can define different transitions for entering and leaving states:

```css
.my-element {
  background: red;
  transition: background 2000ms ease-in; /* exit */
}
.my-element:hover {
  background: blue;
  transition: background 150ms ease;     /* enter */
}
```

<br>

### 🔹 8. Accessibility

* Some users are sensitive to motion.
* <mark>Use `prefers-reduced-motion` to disable transitions for them:</mark>

```css
@media (prefers-reduced-motion: reduce) {
  .my-element { transition: none; }
}
```

<br>

### 🔹 9. Performance Tips

* Best properties: `transform`, `opacity` (cheap, GPU accelerated).
* <mark>Avoid animating layout-affecting properties (`width`, `height`, `margin`) → causes reflow/repaint, slower.</mark>

## Examples
<details>
  <summary>Code</summary>

  ```html
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Transitions Demo</title>
    <style>
      body {
        font-family: sans-serif;
        background: #f4f4f9;
        padding: 20px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 20px;
      }
      .card {
        background: white;
        border-radius: 12px;
        padding: 20px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        text-align: center;
        transition: box-shadow 0.3s ease;
      }
      .card:hover {
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.25);
      }
      h2 {
        font-size: 1.2rem;
        margin-bottom: 10px;
      }
      .demo {
        width: 100px;
        height: 100px;
        margin: 10px auto;
        border-radius: 8px;
        background: #007bff;
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        cursor: pointer;
      }

      /* 1. transition-property */
      .property-demo {
        transition-property: background-color;
        transition-duration: 1s;
      }
      .property-demo:hover {
        background-color: #ff5722;
      }

      /* 2. transition-duration */
      .duration-demo {
        transition: transform 2s;
      }
      .duration-demo:hover {
        transform: rotate(45deg);
      }

      /* 3. transition-timing-function */
      .timing-demo {
        transition: transform 1.5s ease-in-out;
      }
      .timing-demo:hover {
        transform: scale(1.5);
      }

      /* 4. transition-delay */
      .delay-demo {
        transition: background 1s ease 1s; /* 1s delay */
      }
      .delay-demo:hover {
        background: #4caf50;
      }

      /* 5. color transition */
      .color-demo {
        transition: background 0.5s ease;
      }
      .color-demo:hover {
        background: #e91e63;
      }

      /* 6. shadow transition */
      .shadow-demo {
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        transition: box-shadow 0.5s ease;
      }
      .shadow-demo:hover {
        box-shadow: 0 12px 30px rgba(0, 0, 0, 0.4);
      }

      /* 7. filter transition */
      .filter-demo {
        filter: grayscale(100%);
        transition: filter 0.8s ease;
      }
      .filter-demo:hover {
        filter: grayscale(0%);
      }

      /* 8. enter vs exit */
      .enter-exit-demo {
        background: #009688;
        transition: background 2s ease-in;
      }
      .enter-exit-demo:hover {
        background: #ffc107;
        transition: background 0.3s ease-out;
      }

      /* 9. accessibility: reduced motion */
      @media (prefers-reduced-motion: reduce) {
        .demo {
          transition: none !important;
        }
      }

      /* 10. performance tip: use transform */
      .performance-demo {
        transition: transform 0.5s ease;
      }
      .performance-demo:hover {
        transform: translateY(-20px) scale(1.1);
      }
    </style>
  </head>
  <body>
    <div class="card">
      <h2>1. transition-property</h2>
      <div class="demo property-demo">Hover</div>
    </div>

    <div class="card">
      <h2>2. transition-duration</h2>
      <div class="demo duration-demo">Hover</div>
    </div>

    <div class="card">
      <h2>3. transition-timing-function</h2>
      <div class="demo timing-demo">Hover</div>
    </div>

    <div class="card">
      <h2>4. transition-delay</h2>
      <div class="demo delay-demo">Hover</div>
    </div>

    <div class="card">
      <h2>5. Color Transition</h2>
      <div class="demo color-demo">Hover</div>
    </div>

    <div class="card">
      <h2>6. Shadow Transition</h2>
      <div class="demo shadow-demo">Hover</div>
    </div>

    <div class="card">
      <h2>7. Filter Transition</h2>
      <div class="demo filter-demo">Hover</div>
    </div>

    <div class="card">
      <h2>8. Enter vs Exit</h2>
      <div class="demo enter-exit-demo">Hover</div>
    </div>

    <div class="card">
      <h2>9. Accessibility (Reduced Motion)</h2>
      <div class="demo color-demo">Hover</div>
    </div>

    <div class="card">
      <h2>10. Performance (Transform)</h2>
      <div class="demo performance-demo">Hover</div>
    </div>
  </body>
</html>

```
</details>

https://github.com/user-attachments/assets/322073bf-e4e2-40e5-818c-205fbb07c452
