

## 🔹 Keyboard Events Basics

* **Not only keyboard inputs matter** → Input can also come from speech, copy/paste, etc.
* For tracking *any input* in `<input>`, use **`input` event**, not just keyboard events.
* Keyboard events are used for **hotkeys, arrow keys, shortcuts**.

<br>

## 🔹 Key Events

* `keydown` → fires **when a key is pressed down** (auto-repeats if held).
* `keyup` → fires **when a key is released**.

<br>

## 🔹 Event Properties

* `event.key` → the **character/meaning** of the key (changes with Shift/language).
* `event.code` → the **physical key location** (same across languages, e.g. `KeyZ`).
* Difference:

  * Pressing **Z** → `event.key = "z"` or `"Z"` depending on Shift; `event.code = "KeyZ"`.
  * German layout swaps Y and Z → same physical key = `"KeyZ"`, but character differs.
* Use:

  * `event.key` → for layout-dependent characters.
  * `event.code` → for hotkeys that should work regardless of layout.

<br>

## 🔹 Special Keys

* Example codes: `"Enter"`, `"Backspace"`, `"ShiftLeft"`, `"ShiftRight"`.
* `event.key` gives meaning (`"Shift"`), while `event.code` gives exact key (`"ShiftLeft"`).
* Some keys (e.g. `Fn`) don’t generate events (handled at hardware/OS level).

<br>

## 🔹 Auto-repeat

* Holding a key → multiple `keydown` events, then **one `keyup`**.
* `event.repeat = true` for repeated `keydown`.

<br>

## 🔹 Default Actions

* Keys often have default actions:

  * Letters → insert character.
  * Delete → removes character.
  * PageDown → scrolls page.
  * Ctrl+S → browser "Save Page" dialog.
* Can block most defaults with `event.preventDefault()`.
* OS-level shortcuts (e.g. Alt+F4) cannot be blocked.

<br>

## 🔹 Input Filtering Example

* Block invalid phone number input with `onkeydown`:

  ```js
  function checkPhoneKey(key) {
    return (key >= '0' && key <= '9') || ['+','(',')','-'].includes(key);
  }
  ```
* Problem: Blocks Backspace, Arrows, Delete.
* Fix: Allow them in whitelist too.
* Still not 100% safe → users can paste invalid text.
* Better approach: also validate on **`input` event**.

<br>

## 🔹 Legacy (Don’t Use)

* Old events: `keypress`, `keyCode`, `charCode` → deprecated.
* Use modern `keydown`, `keyup` with `key` and `code`.

<br>

## 🔹 Mobile Keyboards

* On virtual keyboards (IME):

  * `event.keyCode = 229`
  * `event.key = "Unidentified"` (often unreliable).
* Some special keys (arrows, backspace) may still work.

<br>

## ✅ Summary

* Events:

  * `keydown` → press (repeats).
  * `keyup` → release.
* Properties:

  * `key` → character meaning.
  * `code` → physical key.
* Use **`key`** if layout matters, **`code`** for consistent hotkeys.
* For form input validation → use **`input` event** instead of only keyboard events.
