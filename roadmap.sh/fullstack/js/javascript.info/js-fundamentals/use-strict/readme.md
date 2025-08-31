
## <mark>**"use strict"**</mark>

- **Purpose**: Introduced in **ES5 (2009)** to fix JavaScript design flaws without breaking old code.  
- **Syntax**: `"use strict";` or `'use strict';`  
  - Must be **at the very top** of the script or function.  
  - Only comments may appear above it.  

<br>

### **Scope**
- Placed at script top → whole script runs in strict mode.  
- Placed inside a function → only that function runs in strict mode.  

<br>

### **Rules**
- If placed **below any code**, it is ignored.  
- Cannot be reverted (no `"no strict"`).  
- Once strict mode is active → it stays active.  

<br>

### **Browser Console**
- Dev tools console runs code in **non-strict mode by default**.  
- To enable:  
  ```js
  'use strict';
  // your code
  ```
  (Use **Shift+Enter** for new lines, then Enter to run.)  
- Alternative (works everywhere):  
  ```js
  (function() {
    'use strict';
    // your code
  })();
  ```

<br>

### **Should We Use It?**
- Yes, it enforces better, safer code.  
- **Modern JavaScript** (`class`, `module`) → strict mode is enabled automatically.  
- For plain scripts, always add `"use strict"` at the top.  
