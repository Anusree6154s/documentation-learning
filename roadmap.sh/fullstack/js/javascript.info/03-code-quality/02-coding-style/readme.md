
### Coding Style – Key Points

* **Curly Braces**: Use Egyptian style (same line as keyword). Example:

  ```js
  if (cond) {
    // ...
  }
  ```
* **Line Length**: Split long lines (strings, conditions). Aim for 80–120 characters max.
* **Indents**:

  * Horizontal: 2 or 4 spaces (spaces preferred).
  * Vertical: use blank lines to separate logical blocks.
* **Semicolons**: Always end statements with semicolons to avoid pitfalls.
* **Nesting Levels**: Reduce deep nesting with `continue` or early `return`.
* **Function Placement**: Usually better to place main code first, helper functions after.
* **Style Guides**: Follow established guides (Google, Airbnb, StandardJS, etc.) for uniformity.
* **Linters**: Use tools (ESLint, JSHint, JSLint) to enforce consistency and catch errors.
