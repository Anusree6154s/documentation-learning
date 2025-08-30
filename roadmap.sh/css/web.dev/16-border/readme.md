

##  Borders in CSS

### 📌 1. Border Basics

* **Border box** = the "frame" around an element in the box model.
* To see a border, you **must define a style** (`solid`, `dashed`, etc.).
* Individual sides: `border-top-style`, `border-right-style`, `border-bottom-style`, `border-left-style`.

<br>

### 📌 2. Border Shorthand

```css
.my-element {
  border: 1px solid red; /* width | style | color */
}
```

Order = **width → style → color**

<br>


### 📌 3. Border Color

* Defaults to `currentColor` (the element’s text color).

```css
.my-element { color: blue; border: solid; } /* border is blue */
```

* Per side: `border-top-color`, `border-right-color`, etc.

<br>


### 📌 4. Border Width

* Named values: `thin`, `medium` (default), `thick`.
* Units: `px`, `em`, `%`, etc.
* Per side: `border-top-width`, `border-right-width`, etc.


<br>

### 📌 5. <mark>Logical Border Properties</mark>

* Flow-relative alternatives:

```css
.my-element {
  border: 2px dotted;
  border-inline-end: 2px solid red; /* right side in LTR, left side in RTL */
}
```
* <mark>Adapts automatically to **text direction (LTR / RTL)**.</mark>

<details>
  <summary>Example</summary>

  
#### problem: 
```html
<!DOCTYPE html>
<html lang="ar" dir="rtl"> <!-- Try changing to dir="ltr" -->
<head>
  <meta charset="UTF-8">
  <title>Border Physical Problem</title>
  <style>
    .box {
      width: 200px;
      padding: 1em;
      border: 2px dotted gray;
      border-right: 2px solid red; /* ❌ always physical right */
    }
  </style>
</head>
<body>
  <div class="box">نص تجريبي</div>
</body>
</html>

```

<img width="301" height="86" alt="image" src="https://github.com/user-attachments/assets/36fc9340-239f-44ad-a970-2a2e3c0c9abb" />

#### solution:
```html
<!DOCTYPE html>
<html lang="ar" dir="rtl"> <!-- Try changing to dir="ltr" -->
<head>
  <meta charset="UTF-8">
  <title>Border Logical Solution</title>
  <style>
    .box {
      width: 200px;
      padding: 1em;
      border: 2px dotted gray;
      border-inline-end: 2px solid red; /* ✅ respects writing direction */
    }
  </style>
</head>
<body>
  <div class="box">نص تجريبي</div>
</body>
</html>

```

<img width="297" height="87" alt="image" src="https://github.com/user-attachments/assets/06dd562b-5f2d-4297-9e1c-0b7e6fc86ad8" />
</details>


<br>



### 📌 6. Border Radius (Rounded Corners)

* Shorthand:

```css
.my-element { border-radius: 1em; }
```

* Per corner:

```css
border-top-left-radius: 1em 2em; /* elliptical radius */
```

* Shorthand multiple corners:

```css
border-radius: 1em 2em 3em 4em; /* TL, TR, BR, BL */
```

* Elliptical with `/`:

```css
border-radius: 95px 155px 148px 103px / 48px 95px 130px 203px;
```

<br>

### 📌 7. <mark>Border Images</mark>

* <mark>Use an **image or gradient** as a border.</mark>

```css
.my-element {
  border-image-source: url('frame.png');
  border-image-slice: 61 58 51 48;  /* slice into 9 parts */
  border-image-width: 20px;
  border-image-outset: 0;
  border-image-repeat: stretch; /* stretch | repeat | round | space */
}
```

#### 🔑 Properties:

* **`border-image-source`** → image or gradient.
* **`border-image-slice`** → slices image into corners, edges, center.
* **`border-image-width`** → thickness of the border.
* **`border-image-outset`** → space between border & element.
* **`border-image-repeat`** → how edges fill space: `stretch`, `repeat`, `round`, `space`.
* **`fill`** keyword → decides if center area is used as background.

<br>

✅ **Summary**:
CSS borders can be styled with solid/dashed/etc., colored, widened, rounded, or even replaced with images/gradients. Logical border properties and border-image offer powerful tools for **internationalization** and **creative designs**.

