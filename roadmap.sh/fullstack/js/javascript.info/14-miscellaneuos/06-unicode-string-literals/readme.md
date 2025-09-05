

## 🔹 Unicode in JavaScript strings

* Strings in JS are based on **Unicode**.
* Each character = sequence of **1–4 bytes**.
* Ways to insert characters:

  1. `\xXX` → 2 hex digits (00–FF, only first 256 chars).

     ```js
     "\x7A" // z
     "\xA9" // ©
     ```
  2. `\uXXXX` → 4 hex digits (0000–FFFF).

     ```js
     "\u044F" // я
     "\u2191" // ↑
     ```
  3. `\u{X…XXXXXX}` → 1–6 hex digits (0–10FFFF). Covers **all Unicode**.

     ```js
     "\u{20331}" // 佫
     "\u{1F60D}" // 😍
     ```

<br>

## 🔹 Surrogate pairs

* JS was built on **UTF-16 (2 bytes per char)** → only 65,536 symbols.
* Rare symbols (> U+FFFF) use **2× 2-byte codes = surrogate pair**.
* Side effects:

  * `.length` shows `2` for one character.
  * Indexing returns meaningless halves.

    ```js
    '😂'.length; // 2
    '𝒳'[0]; // garbage
    ```
* Detectable ranges:

  * First part: `0xD800..0xDBFF`
  * Second part: `0xDC00..0xDFFF`

<br>

## 🔹 Correct handling methods

* Old methods (`charCodeAt`, `fromCharCode`) → **not surrogate aware**.
* New methods (`codePointAt`, `fromCodePoint`) → **handle pairs correctly**.

```js
'𝒳'.charCodeAt(0).toString(16);   // d835 (half only ❌)
'𝒳'.codePointAt(0).toString(16);  // 1d4b3 (full ✅)
```

<br>

## 🔹 String splitting danger

* Splitting at arbitrary positions may break surrogate pairs.

  ```js
  'hi 😂'.slice(0,4); // shows broken half of emoji
  ```

<br>

## 🔹 Diacritical marks & normalization

* Some letters are built as **base char + mark(s)**.

  ```js
  'S\u0307'       // Ṡ (S + dot above)
  'S\u0307\u0323' // Ṩ (S + dot above + dot below)
  ```
* Same-looking chars can be stored differently (different order of marks).

  ```js
  let s1 = 'S\u0307\u0323';
  let s2 = 'S\u0323\u0307';
  s1 == s2; // false ❌
  ```
* Solution: **Unicode normalization** → `str.normalize()`.

  ```js
  "S\u0307\u0323".normalize() == "S\u0323\u0307".normalize(); // true ✅
  ```
* Sometimes normalization compresses multiple chars into one combined symbol (if common enough).

<br>

## 🔹 Key takeaways

* Unicode characters may take **1–4 bytes**.
* Rare symbols = **surrogate pairs** (appear as length `2`).
* Use `codePointAt` / `fromCodePoint` for correct processing.
* Splitting strings blindly is unsafe.
* Diacritical marks may create **different representations of same symbol**.
* Use `normalize()` to compare safely.
