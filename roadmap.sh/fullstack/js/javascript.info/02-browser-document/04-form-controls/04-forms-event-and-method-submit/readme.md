

### 📝 Form submission basics
- A form can be submitted in **two ways**:  
  1. Clicking `<input type="submit">` or `<input type="image">`.  
  2. Pressing **Enter** inside an input field.  

- Both trigger the **`submit` event** on the `<form>`.  

- In the `submit` handler, you can:  
  - Validate input.  
  - Call `event.preventDefault()` to stop submission.  

<br>

### 🔄 Relation between submit & click
- If submission is triggered by **Enter**, a `click` event is fired on the submit button.  
- Even though the button wasn’t physically clicked → the event is still dispatched.  

<br>

### ⚡ Manual form submission
- Call `form.submit()` in JavaScript to send the form programmatically.  
- **Important:** `form.submit()` does **not** trigger the `submit` event.  
  - Assumption: developer already handled validation.  

- Example use case → dynamically create and send a form:  
  ```js
  let form = document.createElement('form');
  form.action = 'https://google.com/search';
  form.method = 'GET';
  form.innerHTML = '<input name="q" value="test">';
  document.body.append(form);
  form.submit();
  ```

<br>

### 🛠️ Task: Modal form (`showPrompt`)
**Requirements:**
- Function `showPrompt(html, callback)` should:  
  1. Display a modal form with message `html`, input field, and buttons **OK** / **CANCEL**.  
  2. If user confirms (Enter or OK): `callback(value)`.  
  3. If user cancels (Esc or CANCEL): `callback(null)`.  
  4. Remove form after interaction.  

- Behavior:  
  - Centered in the window.  
  - Modal → block interaction with page until closed.  
  - Autofocus on `<input>`.  
  - Tab / Shift+Tab cycles focus **within modal only**.  

- Example usage:  
  ```js
  showPrompt("Enter something<br>...smart :)", function(value) {
    alert(value);
  });
  ```

<br>

✅ **Summary**
- `submit` event → validate, prevent default if needed.  
- Enter key also triggers a hidden click on submit button.  
- `form.submit()` → programmatic send, no event fired.  
- Modal form task → requires creating a custom prompt with modal behavior and controlled focus.  
