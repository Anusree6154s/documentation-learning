

### **1. <mark>Shapes in CSS</mark>**

* Shapes can be defined using the **`clip-path`** property.
* Two categories:

  * **Basic shapes** → `circle()`, `ellipse()`, `rect()`, `inset()`, `polygon()`.
  * **Complex shapes** → `path()`, `shape()` (limited browser support).

#### **Basic shapes**

* `circle(r at pos)` → creates circular clip.
* `ellipse(rx ry at pos)` → creates oval clip.
* `rect(top, right, bottom, left)` → rectangle with fixed sides.
* `inset(top right bottom left round radius)` → rectangle inset from edges, responsive.
* `polygon(x y, …)` → any polygon, e.g., triangle, star.

```html
<div class="circle"></div>
<div class="ellipse"></div>
<div class="rect"></div>
<div class="inset"></div>
<div class="polygon"></div>

<style>
div {
  width: 100px;
  height: 100px;
  background: steelblue;
  margin: 10px;
  display: inline-block;
}

/* Circle */
.circle {
  clip-path: circle(50%);
}

/* Ellipse */
.ellipse {
  clip-path: ellipse(50% 30% at center);
}

/* Rectangle using rect() */
.rect {
  clip-path: rect(20px, 80px, 80px, 20px);
}

/* Inset rectangle with rounded corners */
.inset {
  clip-path: inset(10px 20px 30px 10px round 20px);
}

/* Polygon (triangle) */
.polygon {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
}
</style>
```


<img width="761" height="230" alt="image" src="https://github.com/user-attachments/assets/e1d095ba-841c-42bb-a994-ff5be081b89c" />

#### **Complex shapes**

* `path("SVG path")` → uses SVG path syntax, not responsive.
* `shape()` → CSS-native path syntax, responsive (not supported in Firefox).

```html
<div class="window"></div>

<style>
.window {
  width: 150px;
  height: 150px;
  background: crimson;
clip-path: path("M 0 200 L 0,75 A 5,5 0,0,1 150,75 L 200 200 z");
}
</style>

```

<img width="192" height="190" alt="image" src="https://github.com/user-attachments/assets/a12c862f-5f85-4f24-b934-fc6aff4d9ef7" />


- This makes a circle rectangle window shape using SVG path syntax.

<br>

### **2. Clipping**

* **`clip-path`** defines which areas of an element are visible (like cutting shapes out of paper).
* Can use:

  * Basic shapes (`circle()`, `ellipse()`, etc.).
  * SVG-defined clip paths (`<clipPath>` inside SVG).
* Only **one clip-path** can be applied → for multiple, use **compound paths** or **masking**.
* Reference box options:

  * `stroke-box` (default) → includes borders.
  * `fill-box` → only inside border.
```html
<img src="https://picsum.photos/300" id="image">

<svg>
  <defs>
    <clipPath id="circle-clip">
      <circle cx="150" cy="100" r="80" />
    </clipPath>
  </defs>
</svg>

<style>
#image {
  clip-path: url(#circle-clip);
}
</style>

```
<img width="214" height="224" alt="image" src="https://github.com/user-attachments/assets/740e27a8-ce83-4e0f-afdf-a7ca6415b9e6" />

- Here the image is clipped to a circle defined in SVG.

<br>

### **3. Masking**

* Defines visibility based on **images/gradients** instead of geometric shapes.
* Uses **`mask-image`**.
* Allows **partial transparency** (unlike clipping).
* Can apply **multiple masks** (comma-separated).
```html
<div class="masked"></div>

<style>
.masked {
  width: 200px;
  height: 200px;
  background: url("https://placekitten.com/300/300");
  mask-image: radial-gradient(circle, rgba(0,0,0,1) 70%, transparent 100%);
  mask-repeat: no-repeat;
  mask-position: center;
  mask-size: cover;
}
</style>

```

<img width="260" height="252" alt="image" src="https://github.com/user-attachments/assets/fdbfbc06-4151-4ff4-9ca3-4c50851e8d81" />

- This makes the photo appear inside a soft circular mask.
  
  <br>
  
#### Mask types

* **Alpha masking** → transparency of pixels decides visibility.
* **Luminance masking** → brightness + transparency decide visibility.

#### Additional properties

* `mask-clip` → which box to mask (default `border-box`).
* `mask-origin` → reference point (like `background-origin`).
* `mask-position`, `mask-size`, `mask-repeat` → behave like background properties.
* `mask-composite` → how multiple masks combine.
* **`mask` shorthand** → set everything at once.


<br>

### **4. Text Flow Around Shapes**

* **`shape-outside`** defines how inline content wraps around floated elements.
* Works with basic shapes, gradients, or images.
* **Important** → clipping/masking does **not** affect layout flow, only visibility.

```html
<div class="float-shape"></div>
<p>
  This is some text that will wrap around the floated circle shape.
  You can see how text flows naturally around the defined shape.
  The shape-outside property works together with clip-path or an image mask.
</p>

<style>
.float-shape {
  float: left;
  width: 150px;
  height: 150px;
  background: lightblue;
  clip-path: circle(50%);
  shape-outside: circle(50%);
  margin: 20px;
}
</style>

```
<img width="802" height="279" alt="image" src="https://github.com/user-attachments/assets/3072fe96-ba68-4b99-8aaa-b92fef9a9c46" />

- The text flows around the circle instead of the rectangle box.

<br>

### **5. Animations with Shapes**

* **`clip-path`** can be animated between shapes (must use same function & number of points).
* **`offset-path`** → lets elements move along a defined path (e.g., `ray()` for line, `polygon()` for shape).
<details>
  <summary>code example</summary>

```html
  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Offset Path Example</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #f0f0f0;
    }

    .box {
      width: 300px;
      height: 300px;
      border: 2px dashed #888;
      position: relative;
    }

    .ball {
      width: 30px;
      height: 30px;
      background: crimson;
      border-radius: 50%;
      position: absolute;

      /* 🚩 Offset path defines the motion curve */
      offset-path: circle(120px at 150px 150px);

      /* Start position */
      offset-distance: 0%;

      /* Animate along path */
      animation: move 5s linear infinite;
    }

    @keyframes move {
      to {
        offset-distance: 100%;
      }
    }
  </style>
</head>
<body>
  <div class="box">
    <div class="ball"></div>
  </div>
</body>
</html>
```

</details>



https://github.com/user-attachments/assets/7e38f32a-0f2c-4164-a41a-2c8111bdd702






<br>

✅ In short:

* **Clipping** = cuts visible areas using geometric shapes.
* **Masking** = controls visibility using pixel transparency/brightness.
* **Shape-outside** = controls how text flows around elements.
* **Animations** = both `clip-path` and `offset-path` can be animated.

