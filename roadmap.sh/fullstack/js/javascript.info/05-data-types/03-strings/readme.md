
## 📌 JavaScript Strings Summary

* **Strings** are textual data (UTF-16 format).

* **Quotes**:

  * `'single'` and `"double"` are the same.
  * `` `backticks` `` support:

    * Template literals with `${...}`
    * Multiline strings
    * Tagged templates

* **Special Characters** (escape sequences):

  * `\n` → Newline
  * `\r\n` → Windows newline
  * \`' " \`\` → Quotes inside strings
  * `\\` → Backslash
  * `\t` → Tab
  * Rare: `\b, \f, \v` (legacy)

* **Length**:

  * `.length` gives number of characters (not a function).

* **Accessing characters**:

  * `str[pos]` or `str.at(pos)` (supports negatives).

* **Iteration**:

  * `for..of` works on strings.

* **Strings are immutable**:

  * You can’t change characters directly, only create new strings.

* **Changing case**:

  * `.toUpperCase()` / `.toLowerCase()`

* **Searching substrings**:

  * `indexOf(substr, pos)` → position or -1
  * `lastIndexOf(substr, pos)` → from right to left
  * `includes(substr, pos)` → true/false
  * `startsWith()` / `endsWith()`

* **Extracting substrings**:

  * `slice(start, end)` → supports negatives
  * `substring(start, end)` → swaps if start > end, negatives → 0
  * `substr(start, length)` → deprecated but works

* **Comparing strings**:

  * By Unicode code points (`codePointAt()`)
  * `localeCompare()` → language-aware comparison

* **Other useful methods**:

  * `trim()` → removes spaces at start & end
  * `repeat(n)` → repeats string

