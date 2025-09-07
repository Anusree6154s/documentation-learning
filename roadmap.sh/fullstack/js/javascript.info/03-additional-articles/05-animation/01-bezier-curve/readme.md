

### 🎯 What are Bezier curves?

* Curves widely used in **computer graphics**, **vector graphics**, **fonts**, **SVG**, and **CSS animations**.
* Defined by **control points** (2, 3, 4, or more).
* **Order of curve = number of control points – 1**.

  * 2 points → linear (straight line).
  * 3 points → quadratic (parabolic).
  * 4 points → cubic.

<br>

### ✨ Properties

* Curve is always inside the **convex hull** of control points.
* Control points usually **don’t lie on the curve** (except first and last).
* Moving control points changes the curve in an **intuitive way**.
* By connecting multiple Bezier curves → **any complex shape** can be created.

<br>

### 🖌️ De Casteljau’s Algorithm (geometric construction)

Recursive algorithm for building Bezier curves.

**Example: 3 control points (quadratic curve):**

1. Draw control points and connect them with segments.
2. For each parameter `t ∈ [0,1]`:

   * Mark points on each segment at distance proportional to `t`.
   * Connect those → new segment.
   * On that new segment, take a point proportional to `t`.
   * That point belongs to the Bezier curve.
3. Repeating this for all `t` forms the curve.

**Example: 4 control points (cubic curve):**

1. Connect points → 3 segments.
2. For each `t`, mark proportional points → gives 2 new segments.
3. Mark proportional points on them → gives 1 new segment.
4. Mark proportional point → curve point.

**General rule:**

* Start with N control points → N-1 segments.
* Iteratively interpolate until only 1 point remains → that’s the curve point.

<br>

### 📐 Mathematical Formulas

* **2 points (linear):**
  `P = (1-t)P1 + tP2`

* **3 points (quadratic):**
  `P = (1−t)²P1 + 2(1−t)tP2 + t²P3`

* **4 points (cubic):**
  `P = (1−t)³P1 + 3(1−t)²tP2 + 3(1−t)t²P3 + t³P4`

For each value of `t` in `[0,1]`, `(x,y)` gives a point on the curve.

<br>

### 🔧 Usage

* **Graphics & design**: modeling, vector editors, fonts.
* **Web**: Canvas, SVG, CSS animations (`cubic-bezier(...)`).
* **Mathematics**: elegant recursive + polynomial definitions.

<br>

### ✅ Summary

* Bezier curves = defined by control points.
* Two equivalent definitions:

  1. **De Casteljau’s algorithm** (geometric, recursive).
  2. **Polynomial formulas** (mathematical).
* Advantages:

  * Intuitive editing by moving control points.
  * Can build smooth complex shapes by joining curves.
  * Widely used in **graphics, animations, and UI design**.
