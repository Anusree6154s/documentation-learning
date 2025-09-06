

### 1. Concept

* **Event delegation** = attach one handler on a common ancestor instead of many handlers on individual elements.
* Use `event.target` to detect where the event happened.

<br>

### 2. Basic Example (highlight table cell)

* Instead of assigning `onclick` to every `<td>`, assign it to `<table>`.
* Use `event.target.closest('td')` to find the correct cell.
* Benefits: works for any number of `<td>`, even dynamically added ones.

<br>

### 3. Handling Nested Elements

* Problem: click might happen inside `<td>` (e.g., on `<strong>`).
* Solution: use `closest('td')` and ensure it belongs to the correct table.

<br>

### 4. Menu with `data-action`

* Example:

  ```html
  <button data-action="save">Save</button>
  <button data-action="load">Load</button>
  ```
* A single handler on the container reads `event.target.dataset.action` and calls the corresponding method.
* Must bind `this` to preserve class context (`this.onClick.bind(this)`).

<br>

### 5. The “Behavior” Pattern

* **Idea:** Use attributes (e.g., `data-counter`, `data-toggle-id`) to describe behaviors declaratively.
* A **document-wide handler** interprets them.
* Example:

  * `data-counter` → increments button value on click.
  * `data-toggle-id` → toggles visibility of an element with given id.
* Advantage: Anyone can add behaviors in HTML without touching JS.

<br>

### 6. Best Practices

* Always use `addEventListener` for document-level handlers (avoid overwriting).
* Behaviors can be combined on the same element.

<br>

### 7. Benefits of Delegation

* Less memory, fewer handlers.
* Flexible → adding/removing elements doesn’t require extra JS.
* Works with dynamic DOM changes (`innerHTML`, AJAX, etc.).

<br>

### 8. Limitations

* Event must **bubble**.
* `event.stopPropagation()` in child handlers breaks delegation.
* Slight CPU overhead (handler checks every event in container).

<br>

### 9. Tasks (practical applications)

1. **Hide messages** → one handler removes a message when its `[x]` button clicked.
2. **Tree menu** → click on a node title expands/collapses its children.
3. **Sortable table** → click on `<th>` sorts rows by column (`data-type="number|string"`).
4. **Tooltip behavior** → show tooltip on `mouseover`, hide on `mouseout`, using `data-tooltip`.
