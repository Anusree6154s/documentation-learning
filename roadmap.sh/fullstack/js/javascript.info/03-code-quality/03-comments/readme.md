

## 📌 JavaScript Comments — Key Points  

### 1. Types of Comments  
- **Single-line** → `// comment`  
- **Multi-line** → `/* ... */`  

<br>

### 2. Bad Comments 🚫  
- Explaining **what the code does** → usually unnecessary.  
- Example of bad use:  

```js
// This code adds 1 to i
i = i + 1;
```

- Rule of thumb:  
  > “If code is so unclear that it needs a comment → rewrite it.”  

<br>

### 3. Recipe: Factor Out Functions  
- Instead of long inline logic with comments, split into functions.  
- Example:  

❌ With comment:  
```js
// check if i is prime
for (let j = 2; j < i; j++) {
  if (i % j == 0) continue;
}
```

✅ Better:  
```js
function isPrime(n) { ... }
```
👉 Function name becomes a **self-explanatory comment**.  

<br>

### 4. Recipe: Create Functions  
- Long blocks of code with “step” comments → better split into functions.  

❌ With comments:  
```js
// add whiskey
for (...) { ... }
// add juice
for (...) { ... }
```

✅ Refactored:  
```js
addWhiskey(glass);
addJuice(glass);
```

<br>

### 5. Good Comments ✅  
Use comments to describe **things code alone cannot show**:  

- **Overall architecture** → big-picture view of components.  
- **Function usage** → parameters, return values, how to call it.  
  - Use **JSDoc** style for this:  
    ```js
    /**
     * Returns x raised to n-th power.
     * @param {number} x 
     * @param {number} n 
     * @return {number}
     */
    function pow(x, n) { ... }
    ```
- **Why the task is solved this way**  
  - Explain non-obvious choices.  
  - Prevents future developers (or yourself) from wasting time “optimizing” back to an inferior solution.  
- **Subtle / tricky parts** → if code looks odd, explain why.  

<br>

### 6. Comments for Tools  
- JSDoc3 (and others) can **generate documentation** from comments.  
- IDEs (like WebStorm, VSCode) use them for **autocompletion + checks**.  

<br>

### 7. Summary 📝  
✅ Write comments for:  
- Architecture (big picture).  
- Function usage (inputs/outputs).  
- Important decisions (“why this way”).  
- Subtle or tricky features.  

❌ Avoid comments for:  
- Obvious “how code works”.  
- Things that should be clear from function/variable names.  