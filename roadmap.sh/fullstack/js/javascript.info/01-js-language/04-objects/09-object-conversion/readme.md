


### 🔹 Why Conversion Happens
- Objects can’t directly participate in math/string operations.  
- JS **auto-converts objects to primitives** when used with operators or functions.  
- Result is **always a primitive**, never another object.  

<br>

### 🔹 Conversion Hints
There are **3 possible “hints”** JS uses:  
1. **"string"** → when string is expected (e.g., `alert(obj)`, property keys).  
2. **"number"** → for math (`+obj`, `obj1 - obj2`, comparisons like `<`, `>`).  
3. **"default"** → when it’s unclear (`obj1 + obj2`, `obj == number`).  
   - In practice, `"default"` ≈ `"number"` except for `Date`.  

<br>

### 🔹 Conversion Algorithm
When an object needs to be converted:  

1. If `obj[Symbol.toPrimitive](hint)` exists → call it.  
2. Otherwise, if hint = **"string"** → try `toString()`, then `valueOf()`.  
3. Otherwise (hint = **"number"** or **"default"**) → try `valueOf()`, then `toString()`.  

<br>

### 🔹 Methods Used
- **`Symbol.toPrimitive(hint)`** → modern, strict (must return a primitive).  
- **`toString()`** → usually for string conversions.  
- **`valueOf()`** → usually for numeric conversions.  
- By default:  
  - `toString()` → `"[object Object]"`.  
  - `valueOf()` → returns the object itself (ignored).  

<br>

### 🔹 Examples
```js
let user = {
  name: "John",
  money: 1000,
  
  [Symbol.toPrimitive](hint) {
    return hint === "string" ? `{name: "${this.name}"}` : this.money;
  }
};

alert(user);      // {name: "John"}   (string conversion)
alert(+user);     // 1000             (number conversion)
alert(user + 500); // 1500            (default conversion)
```

Alternative with old methods:
```js
let user = {
  name: "John",
  money: 1000,
  toString() { return `{name: "${this.name}"}`; },
  valueOf() { return this.money; }
};
```

<br>

### 🔹 Important Notes
- Methods can return **any primitive** (string, number, boolean, symbol, bigint).  
- Must **not return objects** (ignored for `toString`/`valueOf`, error for `Symbol.toPrimitive`).  
- For debugging/logging → usually enough to implement just `toString()`.  
- Dates are the special case: `"default"` hint is treated like `"string"`.  

<br>

✅ **Summary:**  
Object → Primitive conversion in JS is automatic. You can customize it via `Symbol.toPrimitive`, `toString`, or `valueOf`. There are 3 conversion “hints”: `"string"`, `"number"`, `"default"`. Always return a primitive, never an object.