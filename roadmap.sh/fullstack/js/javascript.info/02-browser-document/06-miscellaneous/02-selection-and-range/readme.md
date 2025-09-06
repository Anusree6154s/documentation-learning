

### 📌 Range Basics

* A **Range** = a pair of boundary points (`start`, `end`).
* Create with `new Range()`.
* Set boundaries with:

  * `range.setStart(node, offset)`
  * `range.setEnd(node, offset)`
* Node can be:

  * **Text node** → offset = character position
  * **Element node** → offset = child index

<br>

### 📌 Range Examples

* Partial text selection:

  ```js
  range.setStart(p.firstChild, 2);
  range.setEnd(p.firstChild, 4); // selects "ll" in "Hello"
  ```
* Element selection:

  ```js
  range.setStart(p, 0);
  range.setEnd(p, 2); // selects Example: <i>italic</i>
  ```
* Different start and end nodes → can span multiple nodes.

<br>

### 📌 Range Properties

* `startContainer`, `startOffset`
* `endContainer`, `endOffset`
* `collapsed` → true if empty
* `commonAncestorContainer` → nearest shared ancestor

<br>

### 📌 Range Methods

* **Set start/end:**

  * `setStart`, `setStartBefore`, `setStartAfter`
  * `setEnd`, `setEndBefore`, `setEndAfter`
* **Quick select:**

  * `selectNode(node)`
  * `selectNodeContents(node)`
  * `collapse(toStart)`
  * `cloneRange()`
* **Editing:**

  * `deleteContents()`
  * `extractContents()`
  * `cloneContents()`
  * `insertNode(node)`
  * `surroundContents(node)`

<br>

### 📌 Selection API

* `document.getSelection()` → Selection object.
* Selection = 0 or more ranges (only Firefox supports multi-range).
* Methods:

  * `getRangeAt(i)`
  * `addRange(range)`
  * `removeRange(range)`
  * `removeAllRanges()` / `empty()`

<br>

### 📌 Selection Properties

* `anchorNode`, `anchorOffset` → start point
* `focusNode`, `focusOffset` → end point
* `isCollapsed` → empty selection?
* `rangeCount`

⚡ Difference:

* **Range** → always start < end.
* **Selection** → can be forward or backward (depends on drag direction).

<br>

### 📌 Selection Methods (shortcuts)

* `collapse(node, offset)` / `setPosition()`
* `collapseToStart()`, `collapseToEnd()`
* `extend(node, offset)`
* `setBaseAndExtent(startNode, startOffset, endNode, endOffset)`
* `selectAllChildren(node)`
* `deleteFromDocument()`
* `containsNode(node, allowPartial)`

<br>

### 📌 Selection Events

* `elem.onselectstart` → when selection begins
* `document.onselectionchange` → whenever selection changes

<br>

### 📌 Working with Form Controls

* Special API for `<input>` and `<textarea>` (simpler, text only).
* Properties:

  * `selectionStart`, `selectionEnd`
  * `selectionDirection` ("forward", "backward", "none")
* Methods:

  * `select()` → select all text
  * `setSelectionRange(start, end, dir)`
  * `setRangeText(replacement, start, end, mode)`

    * mode = `"select" | "start" | "end" | "preserve"`

<br>

### 📌 Examples

* **Track selection:**

  ```js
  area.onselect = () => {
    console.log(area.selectionStart, area.selectionEnd);
  };
  ```
* **Move cursor:**

  ```js
  area.selectionStart = area.selectionEnd = 10;
  ```
* **Wrap selection:**

  ```js
  input.setRangeText(`*${selected}*`);
  ```
* **Insert at cursor:**

  ```js
  input.setRangeText("HELLO", pos, pos, "end");
  ```

<br>

### 📌 Making Elements Unselectable

1. CSS: `user-select: none`
2. Prevent `onselectstart` or `mousedown`
3. Clear selection via `document.getSelection().empty()` (rarely used)

<br>

✅ **Summary:**

* Use **Range** for generic DOM selections.
* Use **Selection API** to control user’s visible selection.
* Use **input/textarea APIs** for text-only selection and cursor management.
