
# 🖱️ Drag’n’Drop with Mouse Events

### 🔹 Why not native drag events?

* HTML5 has native `dragstart`, `dragend`, etc.
* Useful for dragging files, but limited:

  * Can’t restrict dragging to certain area/direction.
  * Poor support on mobile.
* Better control with **custom mouse-based drag’n’drop**.

<br>

### 🔹 Basic Algorithm

1. **`mousedown`** → prepare element for dragging.

   * Make `position:absolute`.
   * Move it into `document.body`.
   * Raise `z-index`.
2. **`mousemove`** → move element by updating `left/top`.
3. **`mouseup`** → stop dragging, clean up event handlers.
4. Disable browser’s native drag (`ondragstart = false`).

<br>

### 🔹 Event Handling

* Track movement on **`document`**, not element.

  * Prevents losing events when mouse moves too fast.

<br>

### 🔹 Correct Positioning

* Problem: element “jumps” to center under pointer.
* Fix: remember initial **shift** between pointer and element corner.

  ```js
  let shiftX = event.clientX - elem.getBoundingClientRect().left;
  let shiftY = event.clientY - elem.getBoundingClientRect().top;
  elem.style.left = event.pageX - shiftX + 'px';
  elem.style.top  = event.pageY - shiftY + 'px';
  ```

<br>

### 🔹 Detecting Drop Targets

* Dragged element covers others → can’t use `mouseover`.
* Solution: `document.elementFromPoint(x, y)`

  * Temporarily hide dragged element (`elem.hidden = true`).
  * Get element below pointer.
  * Show element again.
* Track **current droppable** in variable and handle `enter/leave` highlights.

<br>

### 🔹 Summary of Core Ideas

* Event flow:
  `mousedown → mousemove → mouseup` (disable native drag).
* Keep pointer shift (`shiftX/shiftY`) for smooth dragging.
* Use `elementFromPoint()` to detect droppable elements under pointer.
* Can extend with:

  * Highlighting droppables.
  * Restricting drag area or direction.
  * Auto-scroll on edges.
  * Event delegation for multiple draggables.

<br>

### 🔹 Tasks

1. **Slider**

   * Drag thumb along track.
   * Should stop at edges.
   * Works even if mouse goes outside track.

2. **Drag superheroes around field**

   * All `.draggable` elements movable.
   * Use event delegation (`document.mousedown`).
   * Auto-scroll page at top/bottom edges.
   * No horizontal scroll.
   * Elements must stay inside window, even on fast moves.
