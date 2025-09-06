

## 🔹 Event Bubbling

* When an event happens on an element → it first runs on that element, then its parent, then ancestors up to `document` and sometimes `window`.
* Example: `FORM > DIV > P`

  * Click on `<p>` → order: `p → div → form`.
* Called **“bubbling”** because the event bubbles upward.
* Most events bubble (exceptions: `focus`, `blur`, etc.).

<br>

## 🔹 `event.target` vs `this` (`event.currentTarget`)

* `event.target` → **the deepest element** that initiated the event (never changes).
* `this` / `event.currentTarget` → **the element whose handler is running now**.
* Example: Click inside `<form>`:

  * `this` = `<form>` (because handler is on form).
  * `event.target` = actual clicked element inside form.

<br>

## 🔹 Stopping Bubbling

* `event.stopPropagation()` → stops event from bubbling further **up**.
* `event.stopImmediatePropagation()` → stops bubbling **and** other handlers on the same element.
* ⚠️ Don’t stop bubbling without a strong reason → may break analytics or other features.

<br>

## 🔹 Event Capturing

* Standard DOM event flow has **3 phases**:

  1. **Capturing** → event travels **down** from root to target.
  2. **Target** → event reaches target.
  3. **Bubbling** → event travels **up** from target to root.
* Handlers normally run in **bubbling phase**.
* To catch in capturing phase →

  ```js
  elem.addEventListener("click", handler, true);
  // true = { capture: true }
  ```

<br>

## 🔹 Order Example (click `<p>`)

* Capturing: `HTML → BODY → FORM → DIV → P`
* Bubbling: `P → DIV → FORM → BODY → HTML`
* Target `<p>` appears in **both phases** (because handler can exist in both).

<br>

## 🔹 Other Notes

* `event.eventPhase` → tells current phase (1=capturing, 2=target, 3=bubbling).
* `removeEventListener` must specify the same phase (`true/false`) as when added.
* Multiple handlers on the same element & phase → run in the order they were added.
* `stopPropagation()` in capturing → stops **both capturing & bubbling** afterwards.

<br>

## ✅ Summary

* Event goes **down (capturing) → target → up (bubbling)**.
* Use **bubbling by default** (more natural, like local → global response).
* `event.target` = where the event happened.
* `this` = where the handler is attached.
* Don’t block bubbling unless absolutely necessary.
* Lays the foundation for **event delegation**.
