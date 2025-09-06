
# 🖱️ Mouse Events in JavaScript

## 1. Main Event Types

* **mousedown / mouseup** → button pressed / released.
* **click** → `mousedown → mouseup` on same element (left button).
* **dblclick** → double click (less used today).
* **contextmenu** → right-click (or keyboard menu key).
* **mouseover / mouseout** → pointer enters / leaves element.
* **mousemove** → fires on every pointer move.

📌 **Order for left-click**: `mousedown → mouseup → click`.

<br>

## 2. Mouse Button Info

* `event.button` → which button triggered the event:

  * `0` = Left, `1` = Middle, `2` = Right, `3` = X1 (Back), `4` = X2 (Forward).
* `event.buttons` → bitmask of all currently pressed buttons.
* ⚠️ `event.which` (old, deprecated): `1`=Left, `2`=Middle, `3`=Right.

<br>

## 3. Modifier Keys

* `event.shiftKey` → Shift pressed.
* `event.altKey` → Alt pressed.
* `event.ctrlKey` → Ctrl pressed.
* `event.metaKey` → Cmd (Mac).
* ✅ Best practice: check `(e.ctrlKey || e.metaKey)` for cross-platform support.

<br>

## 4. Coordinates

* **clientX / clientY** → relative to **viewport (window)**.
* **pageX / pageY** → relative to **document** (doesn’t change with scroll).

<br>

## 5. Preventing Defaults

* `mousedown` default → text selection.

  * Use `onmousedown = () => false` to prevent unwanted selection.
* Prevent copying: use `oncopy = () => false`.

<br>

## 6. Mobile Devices

* Mouse events are **emulated** on touch devices for compatibility.

<br>

## 7. Task: Selectable List

### Requirements

* **Single click** → select element, deselect others.
* **Ctrl/Cmd + click** → toggle selection of that element only.
* Prevent native text selection.

### Example Solution

```js
ul.onclick = function(event) {
  if (event.target.tagName !== "LI") return;

  if (event.ctrlKey || event.metaKey) {
    event.target.classList.toggle("selected");
  } else {
    for (let li of ul.querySelectorAll("li")) {
      li.classList.remove("selected");
    }
    event.target.classList.add("selected");
  }
};

ul.onmousedown = () => false; // prevent text selection
```
