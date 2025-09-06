

## 🔹 Focus & Blur Basics

* `focus` → when element gains focus (clicked or Tab).
* `blur` → when element loses focus.
* `<input autofocus>` → focus by default on load.
* Typical use:

  * `focus` → prepare for input, hide old errors.
  * `blur` → validate input, save/send data.

<br>

## 🔹 Methods

* `elem.focus()` → programmatically focus.
* `elem.blur()` → remove focus.
* Cannot prevent losing focus with `preventDefault()`.
* Be careful with forcing focus back (bad UX).

<br>

## 🔹 JS-initiated Focus Loss

* `alert` steals focus → blur happens, then refocus after dismiss.
* Removing element from DOM → blur fires, focus doesn’t return.

<br>

## 🔹 Focusing Any Element (tabindex)

* Default focusable: `<input>`, `<button>`, `<a>`, etc.
* `tabindex` makes *any element* focusable.

  * `tabindex="1+"` → custom tab order.
  * `tabindex="0"` → focusable, default order.
  * `tabindex="-1"` → focusable only via JS (`elem.focus()`), ignored by Tab.
* `elem.tabIndex` works in JS too.

<br>

## 🔹 Delegation

* `focus` & `blur` **do not bubble**.
* Solutions:

  1. Use **capturing phase** (`addEventListener("focus", handler, true)`).
  2. Use `focusin` / `focusout` → same events, but they bubble.

<br>

## 🔹 Extra

* Current focused element: `document.activeElement`.

<br>

## 🔹 Summary

* Use `focus/blur` for validation and UX.
* Use `tabindex` to make elements focusable.
* Use `focusin/focusout` (or capturing) for delegation.
* Avoid breaking natural focus flow (don’t trap users).
