

## 🔗 **Anchor Positioning in CSS (Summary)**

**Problem it solves:**
Before, to align tooltips, dropdowns, modals, etc. with a button/anchor, we had to use:

* `position: absolute` + `top/left` with `getBoundingClientRect()` in JS
* Or hacky offsets with margins/transforms

**Now:**
We can *declare in CSS* that “this floating element is positioned relative to that element.”

<br>

### ✅ Example 1: <mark>Basic Anchor</mark>

```html
<button id="btn">Click me</button>
<div id="tooltip">I’m a tooltip</div>
```

```css
#btn {
  anchor-name: --trigger; /* declare the anchor */
}

#tooltip {
  position: absolute;        /* take out of flow */
  position-anchor: --trigger;/* tether to button */
  position-area: block-end;  /* place below */
  background: black;
  color: white;
  padding: 6px 10px;
  border-radius: 4px;
}
```
<img width="106" height="76" alt="image" src="https://github.com/user-attachments/assets/abdaaaf1-20a7-4597-819b-238d7723afac" />


👉 Tooltip sticks to the button **without JS**.

<br>


### ✅ Example 2: <mark>Implicit Anchors with Popovers</mark>

```html
<button popovertarget="menu">Open Menu</button>
<div id="menu" popover>Menu Items</div>
```

```css
#menu {
  position-area: block-end; /* automatically tethered to button */
  margin: unset;            /* override default popover margin */
  background: white;
  border: 1px solid gray;
  padding: 10px;
}
```

https://github.com/user-attachments/assets/9cb88a18-94da-459d-b9c0-63ff291ec9a4

👉 No need for `position-anchor` — popovers automatically use their trigger as the anchor.

<br>


### ✅ Example 3: <mark>Scoping Anchors</mark>

If you have **multiple dropdowns** with the same `--menu-anchor` name, you can scope them:

```html
<ul>
  <li>
    <button class="menu-btn">Item 1</button>
    <div class="dropdown">Dropdown 1</div>
  </li>
  <li>
    <button class="menu-btn">Item 2</button>
    <div class="dropdown">Dropdown 2</div>
  </li>
</ul>
```

```css
li {
  anchor-scope: --menu-anchor;
}

.menu-btn {
  anchor-name: --menu-anchor;
}

.dropdown {
  position: absolute;
  position-anchor: --menu-anchor;
  position-area: block-end;
}
```
<img width="119" height="88" alt="image" src="https://github.com/user-attachments/assets/dda7c054-4094-4c81-8533-d589c310f570" />

👉 Each dropdown only matches its **sibling button**, not the last button in the DOM.

<br>


### ✅ Example 4: Fallbacks

If the dropdown would overflow at the bottom, flip it above:

```css
.dropdown {
  position: absolute;
  position-anchor: --menu-anchor;
  position-area: block-end;
  position-try-fallbacks: block-start;
}
```

👉 Browser first tries “below” (`block-end`). If it overflows, it falls back to “above” (`block-start`).

<br>

### ✅ Example 5: Using `anchor()` for Fine Control

```css
.tooltip {
  position: absolute;
  position-anchor: --btn;
  left: anchor(--btn inline-start);
  top: calc(anchor(--btn block-end) + 8px); /* offset 8px below */
}
```

👉 Unlike `position-area`, here we **calculate exact offsets**.



💡 **So the flow is:**

1. Give anchor element an `anchor-name`.
2. Floating element → `position: absolute|fixed` + `position-anchor`.
3. Control placement with `position-area`, or precise values with `anchor()`.
