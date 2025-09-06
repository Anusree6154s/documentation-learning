

### 1. DOM Node Classes & Hierarchy
- **Root:** `EventTarget` → base for all event-supporting objects.  
- **Node** → abstract base for all DOM nodes (parentNode, childNodes, etc.).  
- **Document** → represents the whole page (entry point to DOM).  
- **CharacterData** → abstract class, inherited by:
  - `Text` (text inside elements).  
  - `Comment` (HTML comments).  
- **Element** → base for all elements (generic element navigation & search).  
  - `HTMLElement` → base for all HTML elements.  
    - Specialized classes like `HTMLInputElement`, `HTMLBodyElement`, `HTMLAnchorElement` etc.  
- Inheritance chain example for `<input>`:  
  `HTMLInputElement → HTMLElement → Element → Node → EventTarget → Object`.

<br>

### 2. Inspecting Node Classes
- `elem.constructor.name` → class name.  
- `instanceof` → check inheritance.  
- `console.log(elem)` → shows DOM tree.  
- `console.dir(elem)` → shows JS object with properties.

<br>

### 3. nodeType (numeric)
- `1` → element node.  
- `3` → text node.  
- `9` → document node.  
- Read-only, old-fashioned way to check node type.

<br>

### 4. nodeName vs tagName
- `tagName` → only for **elements**.  
- `nodeName` → for **all nodes**:
  - Same as `tagName` for elements.  
  - Other values for non-elements (`#comment`, `#document`).  
- Always **uppercase in HTML mode**, case-sensitive in XML mode.

<br>

### 5. innerHTML
- Returns/sets HTML inside an element.  
- Browser auto-corrects invalid HTML.  
- `<script>` inside innerHTML is inserted but **not executed**.  
- `innerHTML += "..."` → full overwrite (old content reloaded, selections lost).

<br>

### 6. outerHTML
- Returns full HTML of the element **including the element itself**.  
- Writing replaces the element in DOM, but variable reference still points to old element (easy mistake).  

<br>

### 7. nodeValue / data
- For **non-element nodes** (text, comment).  
- Both almost the same, usually use `data`.  
- Example:  
  ```js
  text.data // text node content
  comment.data // comment text
  ```

<br>

### 8. textContent
- Returns only the **text** inside, tags removed.  
- Writing inserts as **plain text** (safe for user input, no HTML injection).  
- Contrast: `innerHTML` treats text as HTML.

<br>

### 9. hidden Property
- Boolean attribute/property, same as `display: none`.  
- Can toggle dynamically:  
  ```js
  elem.hidden = true;
  setInterval(() => elem.hidden = !elem.hidden, 1000);
  ```

<br>

### 10. Other Properties
- Depend on element class.  
- Examples:  
  - `<input>` → `.value`, `.type`.  
  - `<a>` → `.href`.  
  - Any element → `.id`.  
- Most HTML attributes have matching DOM properties.

<br>

### 11. Summary
- Each DOM node belongs to a **class hierarchy**.  
- Main properties:  
  - `nodeType` (1,3,9).  
  - `nodeName/tagName` (element name or node type).  
  - `innerHTML`, `outerHTML`.  
  - `nodeValue/data` (for text/comment).  
  - `textContent` (plain text only).  
  - `hidden` (show/hide).  
- Elements also have **class-specific properties** (`value`, `href`, etc.).  
