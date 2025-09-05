

### 📌 Export Types

1. **Before declaration**

   ```js
   export let value = 42;
   export function sayHi() {}
   export class User {}
   ```

   * No semicolon needed after `export function` / `export class`.

2. **Standalone export**

   ```js
   function sayHi() {}
   function sayBye() {}
   export { sayHi, sayBye };
   ```

3. **Export with alias (`as`)**

   ```js
   export { sayHi as hi, sayBye as bye };
   ```

4. **Default export** (only one per file)

   ```js
   export default class User {}
   export default function() {}
   export default ['Jan', 'Feb', ...];
   ```

   * Can omit the name (since only one default exists).
   * Can also do:

     ```js
     export { sayHi as default };
     ```

<br>

### 📌 Import Types

1. **Named imports**

   ```js
   import { sayHi, sayBye } from './say.js';
   import { sayHi as hi } from './say.js';
   ```

2. **Default import**

   ```js
   import User from './user.js';
   import { default as User } from './user.js';
   ```

3. **Import all**

   ```js
   import * as say from './say.js';
   say.sayHi();
   ```

4. **Import only for side effects (no bindings)**

   ```js
   import './module.js';
   ```

<br>

### 📌 Re-export

1. **Re-export named exports**

   ```js
   export { sayHi, sayBye } from './say.js';
   ```
2. **Re-export default under a name**

   ```js
   export { default as User } from './user.js';
   ```
3. **Re-export everything**

   ```js
   export * from './say.js';         // ignores default
   export { default } from './say.js'; // adds default
   ```

<br>

### 📌 Named vs Default Exports

* **Named exports** → explicit, consistent, force correct names.
* **Default exports** → flexible, but can cause inconsistent naming across team members.
* Some teams avoid default exports for this reason.

<br>

### 📌 Notes

* Imports/exports must be at **top-level** (not inside `if`/functions).
* Build tools (webpack, etc.) remove unused imports automatically (tree-shaking).
* Usual practice: keep imports at top for readability, though technically order doesn’t matter.

<br>

✅ **Summary Table**

| Feature              | Syntax Example                          |
| <br><br><br><br><br><br>-- | <br><br><br><br><br><br><br><br><br><br><br><br><br> |
| Export named         | `export {x, y}`                         |
| Export default       | `export default class {}`               |
| Re-export named      | `export {x} from './mod.js'`            |
| Re-export all        | `export * from './mod.js'`              |
| Re-export default    | `export {default as X} from './mod.js'` |
| Import named         | `import {x} from './mod.js'`            |
| Import default       | `import X from './mod.js'`              |
| Import all           | `import * as obj from './mod.js'`       |
| Import only run code | `import './mod.js'`                     |
