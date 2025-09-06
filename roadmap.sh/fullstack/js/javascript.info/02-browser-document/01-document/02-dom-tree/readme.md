

## 🔹 DOM Tree Basics

* HTML is represented inside the browser as a **DOM (Document Object Model) tree**.
* Every HTML tag = an **object** (element node).
* Nested tags = **children** of the enclosing tag.
* Text inside tags = **text nodes**.
* Everything in HTML (including comments, whitespace, and `<!DOCTYPE>`) becomes part of the DOM.

<br>

## 🔹 Example: Simple HTML

```html
<!DOCTYPE HTML>
<html>
<head>
  <title>About elk</title>
</head>
<body>
  The truth about elk.
</body>
</html>
```

DOM structure:

* `<html>` → root.
* `<head>` and `<body>` → children of `<html>`.
* `<title>` contains a **text node** (`"About elk"`).
* Text like spaces (`␣`) and newlines (`↵`) are also valid text nodes.

<br>

## 🔹 Key Details

* **Spaces/newlines**:

  * Before `<head>` → ignored.
  * After `</body>` → moved inside `<body>` automatically.
* If spaces exist → become text nodes in DOM.
* Removing them → removes corresponding text nodes.

<br>

## 🔹 Autocorrection by Browser

* Browser fixes malformed HTML automatically.
* Example:

  ```html
  <p>Hello
  <li>Mom
  <li>and
  <li>Dad
  ```

  Becomes proper DOM with `<p>` and `<li>` closed.
* Tables always get a `<tbody>` in DOM, even if missing in HTML.

<br>

## 🔹 Node Types

1. **document** → entry point (represents the whole document).
2. **element nodes** → tags (`<div>`, `<p>`, `<body>`).
3. **text nodes** → actual text inside elements.
4. **comment nodes** → `<!-- comment -->`, included in DOM but not shown.
   (There are 12 total types, but these 4 are most used.)

<br>

## 🔹 Developer Tools

* Browser dev tools (Elements tab) let you:

  * Inspect DOM structure.
  * Edit text, attributes, CSS in-place.
  * See styles (`Styles` tab) and computed CSS (`Computed` tab).
  * Check **event listeners** attached to nodes.
* Blank text nodes (spaces/newlines) are usually hidden to save space.

<br>

## 🔹 Console Interaction

* Last selected element in Elements tab = `$0` (previous = `$1`, etc.).
* Example:

  ```js
  $0.style.background = 'red'; // makes selected element red
  ```
* Use `inspect(node)` to jump from console → Elements tab.
* Printing `document.body` in console shows the DOM node.

<br>

## 🔹 Summary

* DOM is a **tree structure** of nodes.
* Tags → element nodes.
* Text → text nodes.
* Comments and even `<!DOCTYPE>` also appear in DOM.
* Browser fixes malformed HTML automatically.
* Developer tools help explore, inspect, and debug DOM.
