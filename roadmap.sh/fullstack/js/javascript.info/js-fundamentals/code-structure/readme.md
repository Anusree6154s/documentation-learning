
## 🧱 Code Structure in JavaScript  

### 1. **Statements**  
- Basic building blocks of code → perform actions.  
- Example:  
  ```js
  alert('Hello');
  alert('World');
  ```  
- Multiple statements can be written on the same line (with semicolons) or separate lines.  

<br>

### 2. **Semicolons (;)**  
- Separate statements.  
- Often optional → JavaScript inserts them automatically (Automatic Semicolon Insertion – ASI).  
- ✅ Example (works fine):  
  ```js
  alert('Hello')
  alert('World')
  ```  
- ⚠️ But not always safe → some cases fail.  

#### Example where ASI works:  
```js
alert(3 +
1
+ 2); // Works → outputs 6
```  

#### Example where ASI fails:  
```js
alert("Hello")

[1, 2].forEach(alert);  // Error
```
- JS interprets it as:  
  ```js
  alert("Hello")[1, 2].forEach(alert);
  ```  
- Fix → always use `;` at the end of statements.  

✅ Recommendation: **Always put semicolons** for safety.  

<br>

### 3. **Comments**  
- Help explain code, make it more readable.  
- Ignored by the JS engine.  

#### Single-line comments:  
```js
// This is a comment
alert('Hello'); // Comment after code
```

#### Multi-line comments:  
```js
/* This is a 
   multi-line comment */
alert('World');
```

#### Commenting out code:  
```js
/* alert('Hello'); */
alert('World'); // Only this runs
```

<br>

### 4. **Hotkeys (in editors)**  
- **Single-line comment** → `Ctrl + /` (Mac: `Cmd + /`).  
- **Multi-line comment** → `Ctrl + Shift + /` (Mac: `Cmd + Option + /`).  

<br>

### 5. **Nested Comments ❌ Not Allowed**  
```js
/*
  /* nested comment ?!? */ // Error
*/
alert('World');
```

<br>

### 6. **Production Note**  
- Comments don’t affect performance.  
- Minifiers remove them before deployment → no impact on production scripts.  

<br>

✅ **Summary:**  
- Use **statements** to perform actions.  
- Always **end with semicolons** (safer).  
- Use **comments** generously → improve readability.  
- Remember: **nested comments not supported**.  

