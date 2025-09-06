

## 🔹 Browser Default Actions  

### Common Default Actions
- **`<a>` click** → navigates to `href`.  
- **Form submit button** → submits form.  
- **Text selection** → drag with mouse.  
- **Right click** → opens browser context menu.  
- **`<input type="checkbox">` click** → checks/unchecks.  
- **`keydown`** → adds character into input.  

<br>

### Preventing Default Actions
- **Main way:** `event.preventDefault()`.  
- **Shortcut (only for `on<event>` inline handlers):** `return false`.  
  ```html
  <a href="/" onclick="event.preventDefault()">here</a>
  <a href="/" onclick="return false">Click</a>
  ```

<br>

### Returning `false` – Exception
- Works **only** in inline `on<event>` attributes.  
- Ignored for handlers set via JavaScript (`elem.onclick = handler`).  
- Returning `true` has no effect.  

<br>

### Follow-up Events
- Preventing one event may cancel the next one:  
  - `mousedown` → leads to `focus`.  
  - If `mousedown.preventDefault()` → no focus.  

<br>

### Passive Handlers
- `addEventListener(event, handler, { passive: true })` → tells browser **not to wait** for `preventDefault()`.  
- Used for performance (e.g., `touchmove` → scrolling).  
- Some browsers default to `passive: true` for `touchstart` & `touchmove`.  

<br>

### `event.defaultPrevented`
- `true` → default action prevented.  
- Useful for delegation:  
  - Instead of `stopPropagation()`, check if already handled.  

<br>

### `stopPropagation()` vs `preventDefault()`
- **`preventDefault()`** → cancels browser’s default action.  
- **`stopPropagation()`** → stops event from bubbling.  
- They are **different and unrelated**.  

<br>

### ⚠️ Best Practices
- Keep elements semantic: `<a>` → navigation, `<button>` → actions.  
- Preventing defaults breaks expected behavior (e.g., right-click, open in new tab). Use carefully.  

<br>

## 🔹 Tasks & Solutions  

### 1. ❓ Why `return false` doesn’t work?  
```html
<script>
  function handler() {
    alert("...");
    return false;
  }
</script>

<a href="https://w3.org" onclick="handler()">the browser will go to w3.org</a>
```
- Here `handler()` is **called**, return value is ignored.  
- Must **return handler’s value directly**:  
  ```html
  <a href="https://w3.org" onclick="return handler()">link</a>
  ```
  ✅ Now `false` is returned to the inline handler → cancels navigation.  
- Or use `event.preventDefault()` inside handler.  

<br>

### 2. ❓ Catch links in element (`id="contents"`)  
- Requirement: Ask confirmation before leaving.  
- Solution with **event delegation**:  
  ```js
  contents.onclick = function(event) {
    let link = event.target.closest('a');
    if (link && contents.contains(link)) {
      let confirmLeave = confirm(`Leave for ${link.href}?`);
      if (!confirmLeave) event.preventDefault();
    }
  };
  ```

<br>

### 3. ❓ Image Gallery  
- Thumbnails update main image.  
- Use **event delegation**:  
  ```html
  <div id="gallery">
    <img id="largeImg" src="img1_large.jpg" alt="">
    <div id="thumbs">
      <a href="img1_large.jpg"><img src="img1_thumb.jpg"></a>
      <a href="img2_large.jpg"><img src="img2_thumb.jpg"></a>
      <a href="img3_large.jpg"><img src="img3_thumb.jpg"></a>
    </div>
  </div>

  <script>
    thumbs.onclick = function(event) {
      let link = event.target.closest('a');
      if (!link) return;
      largeImg.src = link.href;
      event.preventDefault();
    };
  </script>
  ```
