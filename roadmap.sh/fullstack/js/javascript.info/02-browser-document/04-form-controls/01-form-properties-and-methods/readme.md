

## 🔹 Form Navigation  

- **Accessing forms**:  
  - `document.forms` → collection of all forms.  
  - Access by **name**: `document.forms.my`.  
  - Access by **index**: `document.forms[0]`.  

- **Accessing elements inside a form**:  
  - `form.elements` → collection of form controls.  
  - Access by **name**: `form.elements.login`.  
  - Access by **index**: `form.elements[0]`.  
  - Shorter way: `form.login`.  

- **Multiple elements with same name** (e.g., radio buttons, checkboxes):  
  - `form.elements.age` → collection of inputs.  

<br>

## 🔹 Fieldsets (`<fieldset>`)  
- `<fieldset>` behaves like a “subform”.  
- `fieldset.elements` → contains its controls.  
- Elements inside fieldset are accessible **both via form and fieldset**.  

<br>

## 🔹 Backreference  
- Every element has `element.form` → reference to its parent form.  

<br>

## 🔹 Form Elements  

### Input & Textarea  
- `input.value` → string value.  
- `input.checked` → boolean (checkbox, radio).  
- `textarea.value` → use this instead of `innerHTML`.  

<br>

### Select & Option  
- `select.options` → collection of `<option>`.  
- `select.value` → value of selected option.  
- `select.selectedIndex` → index of selected option.  
- **Multiple select (`multiple`)** → get selected options via loop or `filter`.  

Example for multiple:  
```js
let selected = Array.from(select.options)
  .filter(option => option.selected)
  .map(option => option.value);
```

<br>

### Creating Options (`new Option`)  
- Syntax:  
  ```js
  let option = new Option(text, value, defaultSelected, selected);
  ```
- `option.text` → text content.  
- `option.value` → value attribute.  
- `option.index` → index in select.  
- `option.selected` → whether selected.  

<br>

## 🔹 Summary  

- **document.forms** → access all forms.  
- **form.elements** → access form controls.  
- **form[name]** → shortcut to element.  
- **element.form** → backreference to parent form.  
- **.value** → for inputs, textarea, select.  
- **.checked** → for checkboxes, radio.  
- **select.options / value / selectedIndex** → ways to handle selects.  
- **new Option(...)** → creates options dynamically.  

<br>

## 🔹 Task: Add an option to `<select>`  

### HTML:  
```html
<select id="genres">
  <option value="rock">Rock</option>
  <option value="blues" selected>Blues</option>
</select>
```

### ✅ Solution:  
```js
let select = document.getElementById('genres');

// 1. Show current selected value and text
let selectedOption = select.options[select.selectedIndex];
alert(selectedOption.value + " : " + selectedOption.text); // blues : Blues

// 2. Add new option
let newOption = new Option("Classic", "classic", true, true);
select.append(newOption);

// Now "Classic" is selected
```
