

### 1. Context
- **Advanced / internal concept** → rarely needed, but explains some edge cases.  
- Deals with how **`this` is preserved or lost** in method calls.  

<br>

### 2. Problem Example
```js
let user = {
  name: "John",
  hi() { alert(this.name); },
  bye() { alert("Bye"); }
};

user.hi(); // ✅ works
(user.name == "John" ? user.hi : user.bye)(); // ❌ this = undefined
```
- Works with `user.hi()` (dot call).  
- Fails when method is **evaluated first** then called.  

<br>

### 3. Why does it happen?
- Calling a method involves **two steps**:
  1. Get the property (`obj.method`).  
  2. Call it (`()`).
- If separated (e.g. stored in a variable), **`this` is lost**:
  ```js
  let hi = user.hi;
  hi(); // ❌ this = undefined
  ```

<br>

### 4. Reference Type (internal mechanism)
- When doing `obj.method`, JavaScript does **not return the function directly**.  
- It creates a hidden **Reference Type value**:  
  ```
  (base, name, strict)
  ```
  - `base` → the object (`user`)  
  - `name` → the property (`"hi"`)  
  - `strict` → whether strict mode is active  

Example:  
```js
user.hi; // internally → (user, "hi", true)
```

<br>

### 5. How `this` is set
- When you call `(obj.method)()`, the **Reference Type** passes the correct object (`obj`) to set `this`.  
- If the reference is discarded (e.g. assignment, expression), only the function is left → `this` is lost.  

<br>

### 6. Key Rule
✅ Works:
```js
obj.method();
obj['method']();
```

❌ Doesn’t work:
```js
let f = obj.method; f();
(obj.method || otherMethod)();
```

<br>

### 7. Fixing Lost `this`
- Use `.bind(obj)` to lock `this`:  
  ```js
  let hi = user.hi.bind(user);
  hi(); // ✅ works
  ```
- Or use arrow functions / wrapper calls depending on use case.  

<br>

### 8. Summary
- **Reference Type** = hidden internal type to keep track of `(object, property, strict)` when accessing properties.  
- Ensures correct `this` only in direct calls (`obj.method()`).  
- Any intermediate operation (assignment, expression) discards the Reference Type → function is detached → `this` lost.  
- Important mainly in subtle cases of dynamic method calls.  
