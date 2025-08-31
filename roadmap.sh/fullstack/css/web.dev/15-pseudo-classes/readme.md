
## Pseudo-classes

* A **pseudo-class** defines a **special state** of an element (e.g., hover, focus, invalid).
* They depend on **user interaction, element position, or document state**.
* Written with a **colon `:`**, e.g., `:hover`, `:first-child`.



### 🔹 Interactive States

* **`:hover`** → when mouse hovers over an element.
* **`:active`** → when an element is being clicked (mousedown, before mouseup).
* **`:focus`** → when an element is focused (e.g., input clicked/keyboard tab).
* <mark>**`:focus-within`** → when element *or its children* are focused.</mark>
* <mark>**`:focus-visible`** → focus shown only when triggered by keyboard</mark>, not mouse (good for accessibility).
* <mark>**`:target`** → element with an `id` that matches the URL </mark>fragment (e.g., `#content`).



### 🔹 Link States (LVHA order)

* **`:link`** → unvisited link.
* **`:visited`** → visited link (limited styling for security).
* **`:hover`** → hovered link.
* **`:active`** → active link (during click).



### 🔹 Form States

* **`:disabled`** → disabled input/button.
* **`:enabled`** → enabled input/button.
* **`:checked`** → checked radio/checkbox.
* <mark>**`:indeterminate`** → checkbox or progress element in mixed state</mark>
* <mark>**`:placeholder-shown`** → input shows placeholder (empty).</mark>
* <mark>**`:valid`** → input passes validation.</mark>
* <mark>**`:invalid`** → input fails validation.</mark>
* <mark>**`:in-range`** → numeric input within `min`–`max`.</mark>
* **`:required`** → input marked `required`.
* <mark>**`:optional`** → input not required.</mark>



### 🔹 Position & Order

* **`:first-child`** / **`:last-child`** → first/last among siblings.
* **`:only-child`** → only child of its parent.
* **`:first-of-type`** / **`:last-of-type`** → first/last element of its type.
* **`:nth-child(n)`** → select element at index `n` (1-based).
* **`:nth-of-type(n)`** → select element at index `n` of that type.
* **`:nth-last-child(n)`** → count from the end.
* **`:only-of-type`** → only element of its type among siblings.



### 🔹 Content-based

* **`:empty`** → selects element with no children (no text, no whitespace).



### 🔹 Advanced Selectors

* **`:is()`** → shorthand for multiple selectors (forgiving).

  * Example: `.post :is(h2, li, img)`
* **`:not()`** → exclude elements.

  * Example: `a:not([class])`
* **`:has()`** → “parent selector,” matches element if it contains something.

  * Example: `form:has(input:valid) label { font-weight: bold; }`



### ⚡ **In short:**

* **Interaction** → `:hover`, `:focus`, `:active`, `:target`
* **Links** → `:link`, `:visited`, `:hover`, `:active`
* **Forms** → `:disabled`, `:checked`, `:valid`, etc.
* **Structure/order** → `:first-child`, `:nth-child()`
* **Content-based** → `:empty`
* **Advanced logic** → `:is()`, `:not()`, `:has()`


