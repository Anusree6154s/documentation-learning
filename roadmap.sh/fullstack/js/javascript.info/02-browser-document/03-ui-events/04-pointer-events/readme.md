
## 🎯 Pointer Events – Summary

### 1. Why Pointer Events?

* Old times: only **mouse events**.
* Then came **touch events** (`touchstart`, `touchend`, `touchmove`) for multi-touch.
* Later, stylus/pen devices → needed even more features.
* Writing code for both mouse + touch = cumbersome.
* **Pointer Events** introduced → one unified system for **mouse, touch, pen**.
* Supported in all major browsers (except old IE10 and Safari 12-).

<br>

### 2. Pointer Event Types

* Similar to mouse events:

  * `pointerdown` → `mousedown`
  * `pointerup` → `mouseup`
  * `pointermove` → `mousemove`
  * `pointerover` → `mouseover`
  * `pointerout` → `mouseout`
  * `pointerenter` → `mouseenter`
  * `pointerleave` → `mouseleave`
* Extra ones:

  * `pointercancel` – browser/device aborts interaction.
  * `gotpointercapture` – element starts capturing.
  * `lostpointercapture` – element stops capturing.

<br>

### 3. Properties of Pointer Events

* Same as mouse (`clientX`, `clientY`, `target`, etc.) plus:

  * `pointerId` → unique ID for each pointer (finger/stylus).
  * `pointerType` → `"mouse"`, `"pen"`, `"touch"`.
  * `isPrimary` → true for the first pointer (main finger).
* Extra device-specific (often unsupported):

  * `width`, `height` → touch area size.
  * `pressure` → 0..1, or 0.5 for click.
  * `tangentialPressure`, `tiltX`, `tiltY`, `twist` (pen-specific).

<br>

### 4. Multi-touch Support

* Each finger → new `pointerId`.
* Example:

  * First finger → `pointerdown` (`isPrimary=true`).
  * Second finger → `pointerdown` (`isPrimary=false`).
* Track gestures by grouping events with the same `pointerId`.

<br>

### 5. `pointercancel` Event

* Fires when browser/device cancels interaction.
* Causes:

  * Device disabled.
  * Orientation change.
  * Browser takes over (e.g., image drag, zoom/pan).
* Solution:

  * Prevent native drag’n’drop → `ondragstart = () => false`.
  * Prevent native gestures → `touch-action: none` in CSS.

<br>

### 6. Pointer Capture

* Forces all events of a given pointerId to go to one element.
* `elem.setPointerCapture(pointerId)` → all pointer events retargeted to `elem`.
* Released on:

  * `pointerup`, `pointercancel`, or `elem.releasePointerCapture()`.
* Benefits:

  * Cleaner code (no need for `document.onmousemove`).
  * Avoids triggering unrelated handlers.

Events:

* `gotpointercapture` – when capture starts.
* `lostpointercapture` – when capture ends.

<br>

### 7. Summary

* Pointer events unify **mouse + touch + pen**.
* Replace `mouse<event>` with `pointer<event>`.
* Use `pointerId` + `isPrimary` for multi-touch.
* Prevent default (`touch-action: none`) to stop browser hijacking.
* Use **pointer capture** for clean drag’n-drop.
* Fully supported in modern browsers.
