## Cascade
### 1. **Cascade Algorithm Steps**

The cascade decides which CSS rule wins when multiple rules apply.
The order of evaluation is:

1. **Position and Order of Appearance**

   * <mark>Later rules override earlier ones</mark> (if everything else is equal).
   * Applies to `<link>`, `<style>`, inline styles, and multiple declarations in the same block.

2. **Specificity**

   * <mark>More specific selectors override less specific ones.</mark>
   * Specificity hierarchy:

     * Inline styles (highest normal specificity)
     * IDs
     * Classes, attributes, pseudo-classes
     * Elements, pseudo-elements (lowest)
   * Specificity is cumulative (multiple selectors add up).

3. **Origin** (<mark>where styles come from</mark>)

   * Lowest → Highest:

     * User agent (browser defaults)
     * Local user styles
     * Author styles (you write them)
     * Author `!important`
     * User `!important`
     * User agent `!important`

4. **Importance**

   * <mark>Order of importance</mark> (lowest → highest):

     * Normal rules
     * Animations
     * `!important` rules
     * Transitions (highest when active)



### 2. **Position & Order Examples**

* Last declaration wins if specificity is equal:

  ```css
  button { color: red; }
  button { color: blue; } /* wins */
  ```
* Inline `style` attributes override external/embedded CSS (but still follow order if multiple values inside).
* Multiple declarations of same property → last valid one wins (useful for fallbacks):

  ```css
  .el {
    font-size: 1.5rem;
    font-size: clamp(1.5rem, 1rem + 3vw, 2rem); /* wins if supported */
  }
  ```


### 3. **Specificity Examples**

* Class beats element:

  ```css
  .my-element { color: red; }  /* wins */
  h1 { color: blue; }
  ```
* ID beats class or element.
* Long selector lists accumulate specificity → harder to override.


### 4. **Origin Example**

* Example priority (lowest → highest):

  * Browser default: `h1 { margin-block-start: 0.83em; }`
  * Framework (e.g. Bootstrap): `h1 { margin-block-start: 20px; }`
  * Author style: `h1 { margin-block-start: 2ch; }`
  * Media query: `h1 { margin-block-start: 1ch; }`
  * User custom style with `!important`: `h1 { margin-block-start: 2rem !important; }` → **this wins**



### 5. **Importance**

* Active transitions > active animations > `!important` > normal rules.
* Animations and transitions can temporarily override even `!important`.

### 6. Diff between author and user
* Diff
  * **Author = developer of the website**
  * **User = person visiting the site**
  * **User `!important` > Author `!important`** (because the user’s needs take priority).
* Diff in styles
  * **Author styles** = what *you* (developer) provide.
  * **User styles** = what *the visitor or browser* provides.
    * Custom stylesheets/extensions (like Stylish, Stylus, or uBlock cosmetic filters).
    * Browser accessibility settings (e.g. increasing default font size, forcing dark mode).


- Example:

```css
/* Author style */
h1 { font-size: 2rem; }

/* User style (via browser extension or OS setting) */
h1 { font-size: 1.2rem !important; } /* wins */
```
