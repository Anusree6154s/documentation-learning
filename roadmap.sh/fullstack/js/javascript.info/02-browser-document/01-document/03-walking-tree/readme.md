

### 🌳 DOM Navigation Summary

1. **Starting point**

   * All DOM operations begin with the `document` object.
   * Key top-level properties:

     * `document.documentElement` → `<html>`
     * `document.body` → `<body>`
     * `document.head` → `<head>`
   * ⚠️ `document.body` can be `null` if the script runs before `<body>` is parsed.

<br>

2. **Children vs. Descendants**

   * **Child nodes** = direct children only.
   * **Descendants** = children + all nested elements.
   * Properties:

     * `elem.childNodes` → all children (including text & comment nodes).
     * `elem.firstChild`, `elem.lastChild`.
     * `elem.hasChildNodes()` → checks if any children exist.

<br>

3. **DOM Collections**

   * `childNodes` is a **collection**, not a real array.
   * Iterable with `for..of`, but lacks array methods (`filter`, `map`, etc.).
   * Convert with `Array.from()` if needed.
   * Collections are **read-only** and usually **live** (update automatically when DOM changes).
   * ⚠️ Don’t use `for..in` on collections.

<br>

4. **Siblings and Parents**

   * `nextSibling` → next node.
   * `previousSibling` → previous node.
   * `parentNode` → parent node.

<br>

5. **Element-only Navigation**

   * Skips text/comment nodes.
   * Properties:

     * `children` → only element children.
     * `firstElementChild`, `lastElementChild`.
     * `previousElementSibling`, `nextElementSibling`.
     * `parentElement` → only element parent (unlike `parentNode`).

<br>

6. **Special case: `<html>`**

   * `document.documentElement.parentNode` → `document`.
   * `document.documentElement.parentElement` → `null`.

<br>

7. **Tables (extra properties)**

   * `table.rows` → all `<tr>`.
   * `table.caption`, `table.tHead`, `table.tFoot`.
   * `table.tBodies` → all `<tbody>`.
   * `tbody.rows` → rows in that section.
   * `tr.cells` → all `<td>/<th>` in a row.
   * `tr.rowIndex` / `tr.sectionRowIndex`.
   * `td.cellIndex` → cell position in row.

<br>

8. **Summary**

   * **All nodes:** `parentNode`, `childNodes`, `firstChild`, `lastChild`, `previousSibling`, `nextSibling`.
   * **Element-only:** `parentElement`, `children`, `firstElementChild`, `lastElementChild`, `previousElementSibling`, `nextElementSibling`.
   * Some element types (like tables, forms) provide **extra navigation properties**.
