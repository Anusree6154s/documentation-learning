

## 🔹 Attributes vs Properties

### DOM Properties

* DOM nodes = JavaScript objects → can hold properties/methods.
* We can create custom ones:

  ```js
  document.body.myData = { name: "Caesar" };
  document.body.sayTagName = function() { alert(this.tagName); };
  ```
* Case-sensitive (`elem.nodeType` not `elem.NoDeTyPe`).

<br>

### HTML Attributes

* Defined in HTML (`id`, `class`, `href` …).
* Standard attributes → create matching DOM properties.
* Non-standard attributes → not auto-converted to properties.

  ```html
  <body id="test" something="non-standard">
  <script>
    document.body.id;        // "test"
    document.body.something; // undefined
  </script>
  ```

<br>

### Working with Attributes

* Methods:

  * `elem.hasAttribute(name)`
  * `elem.getAttribute(name)`
  * `elem.setAttribute(name, value)`
  * `elem.removeAttribute(name)`
* `elem.attributes` → iterable collection of all attributes.
* Attribute names = **case-insensitive**, values = always **strings**.

<br>

### Property-Attribute Synchronization

* Standard attributes usually sync with properties both ways.
* Exceptions:

  * `input.value`: attribute → property works, property → attribute does NOT.
* Example:

  ```js
  input.setAttribute("id", "id");  // syncs → input.id = "id"
  input.id = "newId";              // syncs → attribute updated
  ```

<br>

### DOM Properties are Typed

* Not always strings. Examples:

  * `input.checked` → boolean
  * `div.style` → object (`CSSStyleDeclaration`)
  * `a.href` → always full URL, even if HTML has relative path.

<br>

### Custom Attributes (`data-*`)

* Safe way to store extra info.
* Accessible via `.dataset`.

  ```html
  <div data-user="John" data-order-state="new"></div>
  <script>
    div.dataset.user;       // "John"
    div.dataset.orderState; // "new"
  </script>
  ```

<br>

### ✅ Summary

* **Properties** → values in DOM objects (typed, case-sensitive).
* **Attributes** → values in HTML (strings, case-insensitive).
* Use **properties** normally. Use **attributes** when:

  1. Working with non-standard attributes.
  2. Need exact HTML-written value (like `href`).

<br>

## 🔹 Tasks

### 1. Get the attribute

```html
<!DOCTYPE html>
<html>
<body>
  <div data-widget-name="menu">Choose the genre</div>
  <script>
    let elem = document.querySelector('[data-widget-name]');
    alert(elem.dataset.widgetName);   // "menu"
    // OR
    alert(elem.getAttribute('data-widget-name')); // "menu"
  </script>
</body>
</html>
```

<br>

### 2. Make external links orange

```html
<!DOCTYPE html>
<html>
<body>
  <ul>
    <li><a href="http://google.com">http://google.com</a></li>
    <li><a href="/tutorial">/tutorial.html</a></li>
    <li><a href="local/path">local/path</a></li>
    <li><a href="ftp://ftp.com/my.zip">ftp://ftp.com/my.zip</a></li>
    <li><a href="http://nodejs.org">http://nodejs.org</a></li>
    <li><a href="http://internal.com/test">http://internal.com/test</a></li>
  </ul>

  <script>
    let links = document.querySelectorAll('a[href]');
    for (let link of links) {
      let href = link.getAttribute('href');
      if (href.includes('://') && !href.startsWith('http://internal.com')) {
        link.style.color = 'orange';
      }
    }
  </script>
</body>
</html>
```
