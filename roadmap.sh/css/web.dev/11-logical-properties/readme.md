
##  Logical Properties in CSS

* **Problem:** <mark>Using physical properties (`margin-right`, `margin-left`, etc.) breaks layouts in right-to-left (RTL) languages.</mark>
  * example:
    * normal flow ltr: <img width="177" height="59" alt="image" src="https://github.com/user-attachments/assets/78571e92-af7e-478f-8206-17be73e38968" />
    * direction rtl: <img width="195" height="60" alt="image" src="https://github.com/user-attachments/assets/1a69d50e-c2d0-4d43-bb3b-3655fa4f5fb9" />


* **Solution:** <mark>Use **logical properties**, which adapt automatically to text direction and writing mode.</mark>
  * after adding `margin-inline-end: 0.5em;` to dot: <img width="186" height="59" alt="image" src="https://github.com/user-attachments/assets/0502b8c6-dd4a-4bc8-b26f-b2ebfb71e6ec" />




### Terminology

* **Physical properties:** `top`, `right`, `bottom`, `left` → fixed directions.
* **Logical properties:** Flow-relative → depend on **writing mode** and **text direction**.



###  Flow Types

* **Block flow:** Direction blocks (like paragraphs) stack.

  * English → **top-to-bottom**.
* **Inline flow:** Direction inline text runs.

  * English → **left-to-right**.
  * Arabic → **right-to-left**.


### 🧩 Flow-Relative Properties

* `margin-top` → `margin-block-start`
* `margin-bottom` → `margin-block-end`
* `margin-left` → `margin-inline-start`
* `margin-right` → `margin-inline-end`


###  Sizing

* Physical: `max-width`, `max-height`, `min-width`, `min-height`
* Logical: `max-inline-size`, `max-block-size`, `min-inline-size`, `min-block-size`



###  Start and End Values

* Use `start` / `end` instead of `left` / `right`.
* Example:

  ```css
  p { text-align: end; }
  ```

  → aligns with **reading direction** instead of physical right.



###  Spacing & Positioning

* Physical:

  ```css
  margin-left: 2em;
  padding-top: 2em;
  top: 0.2em;
  ```

* Logical:

  ```css
  margin-inline-start: 2em;
  padding-block-start: 2em;
  inset-block-start: 0.2em;
  ```

* Shorthand:

  ```css
  margin-inline: 2em 0;
  padding-block: 2em;
  inset-block: 0.2em 0;
  ```


###  Borders & Radius

* Physical:

  ```css
  border-bottom: 1px solid red;
  border-right: 1px solid red;
  border-bottom-right-radius: 1em;
  ```
* Logical:

  ```css
  border-block-end: 1px solid red;
  border-inline-end: 1px solid red;
  border-end-end-radius: 1em;
  ```

---

### 📏 Units

* `vi` = 1% of viewport **inline** size (like `vw`).
* `vb` = 1% of viewport **block** size (like `vh`).
* These adapt to writing direction.



### 🛠 Practical Usage

* Logical properties improve **internationalization**, **flexibility**, and **maintainability**.
* Example: chart axis labels → same margin rules apply in both horizontal and vertical modes.



###  Solving the Icon + Text Issue

❌ Physical property:

```css
p svg { margin-right: 0.5em; }
```

✅ Logical property:

```css
p svg { margin-inline-end: 0.5em; }
```

→ Works in **both LTR and RTL** text directions.

