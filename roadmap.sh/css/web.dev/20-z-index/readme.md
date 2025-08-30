
## 🔹 Z-index and Stacking Contexts

* `z-index` controls **layer order** along the **Z axis** (3D depth).
* Higher value = appears **in front**.
* If **no z-index**, order follows **document source order** (later elements sit above earlier ones).

- ⚠️ To use `z-index`, element usually needs `position` ≠ `static`.
- 👉 Exception: <mark>flex and grid items can use `z-index` without needing `position`.</mark>

<br>

### 🔹 Negative z-index

* Allows element to sit **behind others**:

  ```css
  .child { position: relative; z-index: -1; }
  ```
* But: if parent has both `position` (not static) + `z-index` (not auto), it **creates a stacking context**.
  → Child **cannot escape** behind the parent, even with `z-index: -999`.

<br>


### 🔹 <mark>Stacking Context</mark>

* **Definition:** A group of elements that move together along the Z axis, relative to their parent.
* Children’s `z-index` values are **relative to the parent’s stacking context**.
* Example:

  * Parent A → `z-index: 1`, child → `z-index: 999`.
  * Parent B → `z-index: 2`, child → `z-index: 2`.
    → Child of Parent B sits **above all children of Parent A**, since **parents define the stacking level**.

- ⚠️ The `<html>` element is the root stacking context → nothing can go behind it.
- 👉 You can place elements behind `<body>` until it creates its own stacking context.

<br>


### 🔹<mark> Ways to Create a New Stacking Context</mark>

1. **Position + z-index** (e.g., `position: relative; z-index: 0;`).
2. **Properties that create composite layers:**

   * `opacity < 1`
   * `transform`
   * `will-change`
   * `filter`
   * `backface-visibility: hidden`
3. Root element `<html>` is always a stacking context.

<details>
  <summary>
    Explanation
  </summary>


## 🔹 What is a **Composite Layer**?

* Think of the browser rendering process as **painting a canvas**.
* Normally, when something changes on the page, the browser may need to **repaint large parts of that canvas**, which can be slow.
* To optimize performance, the browser sometimes creates **separate layers** (like sticky notes or transparent sheets) that can be **moved, transformed, or faded independently**.
* These are called **composite layers**.

👉 Examples of properties that trigger a new composite layer:

* `transform`
* `opacity < 1`
* `will-change`
* `filter`
* `backface-visibility: hidden`



## 🔹 Relation to **z-index**

* When an element becomes its **own composite layer**, the browser effectively **creates a new stacking context** for it.
* This means:

  * The element and its children are grouped **together on one layer**.
  * Their `z-index` values are **resolved only inside that group**, not against elements outside.
  * So even if a child inside has `z-index: 9999`, it **cannot escape above another sibling’s stacking context** with a higher parent layer.



## 🔹 Simple Analogy

Imagine your webpage as a **stack of transparent sheets**:

* By default, all elements are drawn on the same sheet, and `z-index` controls which item is "inked" on top.
* If you use `transform`/`opacity`/etc., the browser says:

  > “This might change often — I’ll put it on a **separate sticky note** (composite layer).”
* Now, `z-index` works **within that sticky note**, but the **whole note itself** has an order relative to other notes.



✅ **In short:**

* A **composite layer** = a separate drawing surface created by the browser for performance.
* It automatically creates a **new stacking context**, which affects how `z-index` works.
* Children cannot "escape" their parent’s layer order with `z-index` — they’re confined inside that stacking context.
</details>

<br>


### 🔹 Composite Layers (Performance Note)

* Browser renders page as a **canvas**.
* <mark>Elements likely to change (`transform`, `opacity`, `will-change`) → moved into separate **GPU-accelerated layers** (like sticky notes).</mark>
* <mark>Helps with performance, but also **creates stacking contexts**.</mark>

<br>


### ✅ **Summary:**

* Use `z-index` to control depth order.
* Parent stacking contexts limit child z-index.
* Many CSS properties (not just `z-index`) can trigger new stacking contexts.
* Understanding this prevents common "why isn’t my `z-index` working?" issues.

