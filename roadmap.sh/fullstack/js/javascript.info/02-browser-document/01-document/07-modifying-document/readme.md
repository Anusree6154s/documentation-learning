
## 🔹 Creating Elements

* `document.createElement(tag)` → creates element node.
* `document.createTextNode(text)` → creates text node.
* `elem.cloneNode(deep)` → clone element (`deep=true` includes children).

<br>

## 🔹 Insertion Methods (Modern)

* `node.append(...nodes or strings)` → end of node.
* `node.prepend(...nodes or strings)` → beginning of node.
* `node.before(...nodes or strings)` → before node.
* `node.after(...nodes or strings)` → after node.
* `node.replaceWith(...nodes or strings)` → replace node.
* Strings inserted as **text**, not HTML (safe).

<br>

## 🔹 Inserting as HTML

* `elem.insertAdjacentHTML(where, html)` → inserts as **HTML**.

  * `"beforebegin"` – before elem.
  * `"afterbegin"` – inside elem, at start.
  * `"beforeend"` – inside elem, at end.
  * `"afterend"` – after elem.
* Variants: `insertAdjacentText`, `insertAdjacentElement` (rare).

<br>

## 🔹 Removing & Moving

* `node.remove()` → removes node.
* Moving an element = just re-inserting → auto-removes from old position.

<br>

## 🔹 Cloning

* `cloneNode(true)` → deep clone (includes children).
* `cloneNode(false)` → shallow clone (no children).

<br>

## 🔹 DocumentFragment

* A lightweight container for nodes.
* Insertion inserts **its children**, not the fragment itself.
* Often replaced with arrays + spread `ul.append(...nodes)`.

<br>

## 🔹 Old-School Methods (legacy)

* `parent.appendChild(node)`
* `parent.insertBefore(node, nextSibling)`
* `parent.replaceChild(newNode, oldNode)`
* `parent.removeChild(node)`
* Return the inserted/removed node.

<br>

## 🔹 `document.write`

* Super old way → inserts raw HTML during parsing.
* Works **only while loading**. After load → erases document.
* Very fast (writes before DOM built).
* Seen in old scripts, not used today.

<br>

## 🔹 Summary

**Create:** `createElement`, `createTextNode`, `cloneNode`
**Insert:** `append`, `prepend`, `before`, `after`, `replaceWith`
**Insert HTML:** `insertAdjacentHTML(where, html)`
**Remove:** `remove()`
**Legacy:** `appendChild`, `insertBefore`, `removeChild`, `replaceChild`
**Old-school:** `document.write` (only while loading).

