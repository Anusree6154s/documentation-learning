
### 🔑 Key Points about `?.` (Optional Chaining)

1. **Purpose**

   * Safely access deeply nested properties.
   * Avoids runtime errors when intermediate properties are `null` or `undefined`.
   * Returns `undefined` instead of throwing an error.

<br>

2. **The Problem Without `?.`**

   ```js
   let user = {};
   alert(user.address.street); // ❌ Error: Cannot read 'street'
   ```

   You’d normally need:

   ```js
   alert(user.address ? user.address.street : undefined); // ✅ Safe but verbose
   ```

<br>

3. **Basic Syntax**

   ```js
   obj?.prop       // Safe property access
   obj?.[prop]     // Safe bracket notation
   obj.method?.()  // Safe method call
   ```

<br>

4. **Examples**

   * **Safe Property Access**

     ```js
     let user = {};
     console.log(user?.address?.street); // undefined (no error)
     ```

   * **Safe DOM Access**

     ```js
     let html = document.querySelector('.elem')?.innerHTML;
     // undefined if no element
     ```

   * **Safe Method Call**

     ```js
     let user = {
       sayHi() { console.log("Hi!"); }
     };

     user.sayHi?.(); // ✅ Runs if exists
     user.sayBye?.(); // ❌ Nothing happens, no error
     ```

   * **Safe Property with Brackets**

     ```js
     let key = "name";
     let user = { name: "Alice" };
     let user2 = null;

     console.log(user?.[key]);  // Alice
     console.log(user2?.[key]); // undefined
     ```

   * **With delete**

     ```js
     let user = { name: "John" };
     delete user?.name; // ✅ Works only if user exists
     ```

<br>

5. **Short-Circuiting**

   * Stops evaluation immediately if the left side is `null`/`undefined`.

   ```js
   let user = null;
   let x = 0;

   user?.sayHi(x++); // sayHi not called
   console.log(x);   // 0 (not incremented)
   ```

<br>

6. **Limitations**

   * Works only for **reading/deleting**, not writing.

   ```js
   let user = null;
   user?.name = "John"; // ❌ Error
   ```

<br>

7. **Best Practices**

   * Use only when absence (`null`/`undefined`) is **expected and acceptable**.
   * Don’t overuse—it may hide bugs.
   * The variable itself must be **declared**:

     ```js
     user?.address; // ❌ ReferenceError if user is not defined
     ```

<br>

8. **Summary**

   * `obj?.prop` → safe property access
   * `obj?.[prop]` → safe bracket property access
   * `obj.method?.()` → safe method call
