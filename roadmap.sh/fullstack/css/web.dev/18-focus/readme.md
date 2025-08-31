
##  Focus

* Focus = the state when an element is active and ready for user interaction.
* Example: links, buttons, form fields automatically get focus when tabbing with keyboard.
* Programmatic focus = applied via JavaScript or URL hash (`#id`).



###  Why is Focus Important?

* Essential for **accessibility** → helps keyboard/switch users know where they are.
* Without visible focus, users can get **lost** or trigger wrong actions.
* Accessible websites must provide **clear focus states**.


###  How Elements Get Focus

* **By default**: `<a>`, `<button>`, `<input>`, `<select>`, etc.
* **Navigation**: `Tab` → move forward, `Shift+Tab` → move backward.
* <mark>**tabindex attribute**:</mark>

  * `tabindex="0"` → element is focusable, follows normal order.
  * `tabindex="-1"` → only programmatically focusable (not in tab order).
  * `tabindex="1"` (or higher) → overrides normal order (not recommended).
  * <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/5fa25c5b-0f80-4fa6-a04d-5d45d2a97d60" />


⚠️ <mark>Always **respect source order** → changing focus order unpredictably is bad for accessibility.</mark>


###  Styling Focus

* Browsers show a **default focus ring** (varies by OS & browser).
* Customize with CSS pseudo-classes:

  * `:focus` → element itself has focus.
  * `:focus-within` → parent element when a child is focused.
  * `:focus-visible` → only show when focus is from keyboard (not mouse).

Example:

```css
a:focus {
  outline: 2px solid slateblue;
  outline-offset: 4px;
}
```

* Use **outline** (preferred).
* Avoid removing focus with `outline: none`.
* Avoid using `box-shadow` alone → not visible in Windows High Contrast Mode.


###  In Summary

1. Focus shows where the user is → vital for accessibility.
2. Use `tabindex` carefully:

   * `0` = normal
   * `-1` = programmatic only
   * `>0` = avoid unless absolutely necessary
3. Always provide **strong, visible focus styles**.
4. Stick with `outline` → it works across accessibility modes.

