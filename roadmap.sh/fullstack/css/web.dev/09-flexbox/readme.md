
##  Flexbox 

* **Flexbox = one-dimensional layout model** (works on a row *or* a column, not both at once).
* Ideal for **responsive layouts** (like sidebar + content).
* Provides **flexible boundaries** instead of rigid dimensions.



##  Features of Flexbox

* Layout direction: **row** or **column**.
* Respects **writing mode** (e.g., LTR, RTL, vertical text).
* Single line by default, can **wrap** with `flex-wrap`.
* Items can be **reordered visually** (`order`, `row-reverse`, etc.).
* Items can **grow, shrink, or stay fixed** based on available space.
* Space can be **distributed inside or around items**.
* Alignment works along **main axis** and **cross axis**.



##  Main Axis vs Cross Axis

* **Main axis** = direction of `flex-direction` (row → horizontal, column → vertical).
* **Cross axis** = perpendicular to main axis.
* Items move as a group on the main axis; alignment happens on the cross axis.



## 📌 Creating a Flex Container

```css
.container {
  display: flex;
}
```

Default behavior:

* Direction: **row**
* **No wrapping** (`flex-wrap: nowrap`)
* Items **don’t grow** to fill space
* Items **align at the start** of container



##  Flex Direction

```css
flex-direction: row | row-reverse | column | column-reverse;
```

⚠️ <mark>Be cautious: reversing flow (`row-reverse`, `order`) may harm **accessibility** (keyboard/screen readers follow DOM order).</mark>



## 📌 Wrapping Items

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
```

* Creates **multiple lines** if items don’t fit.
* Still one-dimensional (rows/columns can’t align across lines).

<mark>Shorthand:`flex-flow: column wrap;`</mark>



## 📌 Flex Item Sizing

* **Defaults**:
  `flex-grow: 0; flex-shrink: 1; flex-basis: auto;`
* Shorthands:

  * `flex: auto` → grow/shrink based on content
  * `flex: 1` → equal sizes (ignore content size)
  * `flex: none` → fixed, no growth/shrinkage

👉 Different growth rates possible:

```css
.item1 { flex: 1; }
.item2 { flex: 2; }
.item3 { flex: 3; }
```



## 📌 Alignment & Space Distribution

### On Main Axis

```css
justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
```

### On Cross Axis

* Align **items individually**:

```css
.item1 { align-self: flex-start; }
```

* Align **items as a group**:

```css
.container { align-items: center; }
```

* Align **wrapped lines**:

```css
.container { align-content: space-between; }
```

<mark>Shorthand:<mark/>

<mark>`place-content: center flex-end;`</mark>

---

## 📌 Centering Items (common use)

```css
.container {
  display: flex;
  justify-content: center; /* horizontal */
  align-items: center;     /* vertical */
}
```



## 📌 <mark>Notes & Best Practices</mark>

* <mark>**No `justify-self` in flexbox** (works in Grid, not Flexbox).</mark>
* <mark>Use **auto margins** to push items apart:</mark>

```css
.item-last { margin-left: auto; }
```

*<mark> Avoid using `order` or `reverse` unless necessary → accessibility risk.</mark>



