

## **User Interaction Functions**

### **alert(message)**

* Shows a modal window with a message.
* Blocks interaction until **OK** is pressed.
* Example:

  ```js
  alert("Hello");
  ```

<br>

### **prompt(title, \[default])**

* Shows a modal window with a message, text input, and **OK/Cancel** buttons.
* **Arguments**:

  * `title`: message shown to the user.
  * `default`: *(optional)* pre-filled text in the input.
* **Return values**:

  * Text entered (string) if **OK**.
  * `null` if **Cancel** or **Esc**.
* Example:

  ```js
  let age = prompt("How old are you?", 18);
  alert(`You are ${age} years old!`);
  ```

<img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/82cf6b83-fc34-42ce-8ad6-4df60efa9471" />

* ⚠️ In **Internet Explorer**, if `default` is omitted → `"undefined"` appears. Always provide a second argument.

<br>

### **confirm(question)**

* Shows a modal window with a question and **OK/Cancel** buttons.
* **Return values**:

  * `true` if **OK** pressed.
  * `false` if **Cancel** or **Esc**.
* Example:

  ```js
  let isBoss = confirm("Are you the boss?");
  alert(isBoss);
  ```
<img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/a625efd4-09a3-4d72-bfe3-395f42b0cbea" />

<br>

## **Summary**

* **alert** → message only.
* **prompt** → asks for text input, returns string or `null`.
* **confirm** → asks a yes/no question, returns `true` or `false`.
* All are **modal**: pause script & block page interaction.
* Style/position → controlled by the browser, not customizable.

<br>

✅ **Task Example – Ask for a Name**

```html
<!DOCTYPE html>
<html>
<head>
  <title>Prompt Example</title>
</head>
<body>
  <script>
    let name = prompt("What is your name?", "");
    alert(`Hello, ${name}!`);
  </script>
</body>
</html>
```
