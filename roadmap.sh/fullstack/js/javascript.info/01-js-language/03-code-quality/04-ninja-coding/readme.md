
## 🥷 Ninja Coding Tricks (Irony Edition)

> ⚠️ These are written tongue-in-cheek — i.e., “what NOT to do” if you want maintainable code.

<br>

### 1. Brevity is the soul of wit
- Make code as **short** as possible, even at the cost of clarity.  
- Example: deeply nested ternary operators.  
- The shorter, the “smarter” (and unreadable) it looks.

<br>

### 2. One-letter variables
- Use **single letters**: `a`, `b`, `c`, `x`, `y`.  
- Avoid the obvious `i` for loops — pick exotic letters instead.  
- Makes searching & understanding harder.

<br>

### 3. Abbreviations everywhere
- Shorten words:  
  - `list → lst`, `userAgent → ua`, `browser → brsr`.  
- Only people with “intuition” can read it.

<br>

### 4. Abstract naming
- Use vague names: `obj`, `data`, `value`, `item`, `elem`.  
- If taken, just add numbers: `data1`, `item2`, `elem5`.  
- Or name by type: `str`, `num`.  

<br>

### 5. Attention test
- Use **similar names**: `date` vs. `data`.  
- Sprinkle typos. Readers get stuck.  

<br>

### 6. Smart synonyms
- Same concept, different words:  
  - `displayMessage`, `showName`, `renderUser`, `paintText`.  
- For unrelated things → use **same prefix** (`printPage` vs `printText`).  

<br>

### 7. Reuse names
- Avoid new variables — **overwrite old ones**.  
- Example: reassign parameter halfway through a function.  
- Forces others to trace carefully.

<br>

### 8. Underscores for fun
- Add `_` and `__` before names with **no consistent meaning**.  
- Use inconsistently in different places.  

<br>

### 9. Show your love
- Use fancy adjectives: `superElement`, `megaFrame`, `niceItem`.  
- Looks impressive, conveys no details.

<br>

### 10. Overlap outer variables
- Shadow variables inside functions:  
  ```js
  let user = authenticateUser();
  function render() {
    let user = anotherValue();
    ...
  }
  ```
- Makes it unclear which variable is being used.

<br>

### 11. Side-effects everywhere
- Functions like `isReady()`, `checkPermission()` should also **modify state** or return unexpected objects.  
- Surprise factor: high 🔥.  

<br>

### 12. Powerful functions
- Don’t limit a function to its name.  
- Example: `validateEmail(email)` should also:
  - Show an error popup.  
  - Ask user to re-enter email.  
- Prevents reuse — mission accomplished.

<br>

## ⚡ Summary
- Follow **some** tricks → code is “interesting.”  
- Follow **many** → code becomes **yours alone**.  
- Follow **all** → nobody else dares touch it.  