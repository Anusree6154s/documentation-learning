
### 🖱️ Mouseover / Mouseout

* **Triggered when:**

  * `mouseover`: mouse enters an element.
  * `mouseout`: mouse leaves an element.

* **Properties:**

  * `event.target` → element being entered/exited.
  * `event.relatedTarget` → the element mouse came from / goes to (can be `null` if from/outside the window).

* **Special behavior:**

  * Fires **even when moving to/from a child element**.
  * Events **bubble up**.
  * Fast movement may **skip intermediate elements**, but if `mouseover` happened, there will always be a corresponding `mouseout`.

<br>

### 🖱️ Mouseenter / Mouseleave

* Similar to `mouseover`/`mouseout`, but:

  * Do **not** fire when moving between parent ↔ child.
  * Do **not bubble**.
  * Simpler to use when only entry/exit of the whole element matters.

<br>

### ⚠️ Key differences

| Feature                       | mouseover/mouseout | mouseenter/mouseleave |
| ----------------------------- | ------------------ | --------------------- |
| Fires on parent → child moves | ✅ Yes              | ❌ No                  |
| Bubbling                      | ✅ Yes              | ❌ No                  |
| Delegation possible           | ✅ Yes              | ❌ No                  |

<br>

### 🧩 Event delegation example (with `mouseover/out`)

* Highlight `<td>` cells in a table:

  * Track current cell.
  * Ignore moves inside the same cell.
  * Trigger `onEnter`/`onLeave` only when entering/leaving the cell as a whole.

<br>

### 💡 Use cases

* **mouseover/out** → complex interactions, event delegation, tracking transitions.
* **mouseenter/leave** → simple UI effects (hover, tooltips, menus).

<br>

✅ **Summary**

* `mouseover/out`: more detailed, bubble, can be delegated, but require filtering (child transitions).
* `mouseenter/leave`: simpler, no bubbling, but no delegation.
* Use `relatedTarget` to know where the pointer is coming from/going to.
