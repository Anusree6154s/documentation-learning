
### 1. Concept

* `MutationObserver` = built-in object to watch DOM changes.
* Triggers callback with a list of **MutationRecord** objects when observed changes occur.

<br>

### 2. Syntax

1. Create observer:

   ```js
   let observer = new MutationObserver(callback);
   ```
2. Start observing:

   ```js
   observer.observe(node, config);
   ```
3. `config` options (booleans):

   * `childList` → watch for children added/removed.
   * `subtree` → watch all descendants.
   * `attributes` → watch attribute changes.
   * `attributeFilter` → array of specific attributes.
   * `characterData` → watch text node changes.
   * `attributeOldValue` / `characterDataOldValue` → provide old value too.

<br>

### 3. MutationRecord Properties

* `type` → `"attributes" | "characterData" | "childList"`.
* `target` → node where change happened.
* `addedNodes` / `removedNodes`.
* `previousSibling` / `nextSibling`.
* `attributeName` / `attributeNamespace`.
* `oldValue` → old data/attribute value (if requested).

<br>

### 4. Example

* Editable `<div>` → detect text changes inside it.
* Mutation log shows either `characterData` changes or `childList` mutations if nodes are removed/added.

<br>

### 5. Usage: Integration

* Useful for handling third-party scripts.
* Example: detect and remove unwanted ads `<div class="ads">`.
* Detect when third-party inserts content → adapt layout dynamically.

<br>

### 6. Usage: Architecture

* Example: Syntax highlighting with Prism.js.
* Static case: highlight snippets on `DOMContentLoaded`.
* Dynamic case: use `MutationObserver` to automatically highlight code snippets when new content (articles, forum posts, etc.) is inserted.

<br>

### 7. Additional Methods

* `observer.disconnect()` → stop observing.
* `observer.takeRecords()` → retrieve unprocessed mutation records (then cleared).

<br>

### 8. Garbage Collection

* Observers use **weak references**.
* Observing a node does **not** prevent its garbage collection if it becomes unreachable.

<br>

### 9. Summary

* `MutationObserver` lets you **react to DOM changes** (attributes, text, children).
* Helps integrate with third-party scripts and manage dynamic content.
* Config options improve performance by filtering what’s observed.
