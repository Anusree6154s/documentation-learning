
### **Event constructor**
- Create events using:
  ```js
  let event = new Event(type, { bubbles, cancelable });
  ```
- **Options:**
  - `bubbles: true/false` → whether event bubbles (default `false`).
  - `cancelable: true/false` → whether `preventDefault()` can be used (default `false`).

<br>

### **dispatchEvent**
- Use `elem.dispatchEvent(event)` to trigger the event.
- Handlers react just like for real browser events.
- If event was created with `bubbles: true`, it will bubble up.

<br>

### **event.isTrusted**
- `true` → real user event.  
- `false` → script-generated event.

<br>

### **Bubbling with custom events**
- Example:
  ```js
  let event = new Event("hello", { bubbles: true });
  elem.dispatchEvent(event);
  ```
- Must use `addEventListener` (no `onhello` shortcut).
- Must set `bubbles: true` if you want bubbling.

<br>

### **Specialized event constructors**
- Use dedicated classes for built-in event types:
  - `MouseEvent`, `KeyboardEvent`, `FocusEvent`, `WheelEvent`, etc.
- Example:
  ```js
  let event = new MouseEvent("click", {
    bubbles: true,
    cancelable: true,
    clientX: 100,
    clientY: 100
  });
  ```
- Generic `Event` ignores extra properties like `clientX`.

<br>

### **CustomEvent**
- Use for **new, custom event types**.
- Supports an extra `detail` property for custom data.
- Example:
  ```js
  elem.dispatchEvent(new CustomEvent("hello", {
    detail: { name: "John" }
  }));
  ```

<br>

### **event.preventDefault()**
- Only works if `cancelable: true` was set.
- Dispatch returns `false` if a handler called `preventDefault()`.
- Useful for cases like confirming before an element hides.

<br>

### **Synchronous nature of dispatchEvent**
- Events dispatched with `dispatchEvent` run **immediately**, before returning to the outer code.
- Example order:
  ```js
  alert(1);
  elem.dispatchEvent(new Event("custom"));
  alert(2);
  // Output: 1 → handler → 2
  ```
- To make it async, wrap in `setTimeout`.

<br>

### **Summary**
- Use `new Event(name, options)` for generic events.  
- Use specialized constructors (`MouseEvent`, etc.) for UI events.  
- Use `new CustomEvent(name, { detail })` for custom component events.  
- `bubbles: true` → event propagates upward.  
- `cancelable: true` → allows `preventDefault()`.  
- Custom events are mainly for **component communication**.  
- Generating built-in events (`click`, `keydown`) is usually bad practice → only for hacks/testing.
