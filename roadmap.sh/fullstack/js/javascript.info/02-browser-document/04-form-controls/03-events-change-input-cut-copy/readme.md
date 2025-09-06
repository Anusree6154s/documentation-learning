

# ✍️ Data Change Events in JavaScript

## 1. `change`

* Fires **after value is committed** (not during typing).
* For `<input type="text">` → fires **on blur (focus loss)**.
* For `<select>`, `<input type="checkbox/radio">` → fires **immediately on change**.

<br>

## 2. `input`

* Fires **on every change of value** (typing, pasting, speech input).
* ✅ Best event to track **live updates** in form fields.
* Doesn’t fire on actions that don’t change value (e.g. arrow keys).
* ❌ `event.preventDefault()` won’t work → happens *after* value change.

<br>

## 3. `cut`, `copy`, `paste`

* Belong to **ClipboardEvent**.
* Allow access to clipboard via `event.clipboardData`.
* Can use `event.preventDefault()` → stops cut/copy/paste.
* ⚠️ In `cut`/`copy`, `event.clipboardData.getData(...)` is empty (data not copied yet).

  * Use `document.getSelection()` instead.
* Clipboard may contain **text, images, files** (via `DataTransfer` interface).

<br>

## 4. Clipboard API

* `event.clipboardData` → works only inside user-initiated events.
* `navigator.clipboard` → modern async API, requires user permission.
* Cannot dispatch fake clipboard events (`dispatchEvent`) → restricted for security.

<br>

## 5. Safety Restrictions

* Clipboard = OS-level global → websites cannot read it freely.
* Browser limits access only during **real user actions** (cut/copy/paste).

<br>

## 6. Summary Table

| Event      | When fires                                                     | Special notes                        |
| ---------- | -------------------------------------------------------------- | ------------------------------------ |
| **change** | On value commit (blur) / immediate for select, checkbox, radio | Not live                             |
| **input**  | On every change (typing, paste, speech)                        | Live update, can’t prevent           |
| **cut**    | User cuts selection                                            | Can `preventDefault()`               |
| **copy**   | User copies selection                                          | Can `preventDefault()`               |
| **paste**  | User pastes data                                               | Access via `clipboardData.getData()` |

<br>

## 7. Task: Deposit Calculator

* Inputs:

  * `initial` → sum of deposit
  * `interest` → yearly % rate
  * `years` → number of years
* Formula:

  ```js
  let result = Math.round(initial * (1 + interest) ** years);
  ```
* Use `input` event on fields → update result immediately.
