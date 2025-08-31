

### 📌 **List Styles**

* `list-style-type`: controls how list markers look (e.g., `decimal`, `upper-roman`, `lower-alpha`, etc.).
* W3C **Ready-made Counter Styles** → adds **181 extra styles** across **45 writing systems**.
* `@counter-style`: lets you **define custom markers** (symbols, prefix, suffix, etc.).
* `list-style-position`:

  * `outside` (default) → marker outside the content box.
  * `inside` → marker inside the content box.

<br>

### 📌 **Counters**

* Every `<li>` has an implicit counter called `list-item`.
* **Creating counters**:

  * `counter-reset`: creates/initializes a counter.
  * `counter-increment`: increases/decreases counter.
  * `counter-set`: sets value of an existing counter.
* **Displaying counters**:

  * `content: counter(name)` → single value.
  * `content: counters(name, ".")` → nested values with separator.

<br>


## Examples
<details>
  <summary>Code</summary>

  ```html
 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Counters & List Styles Demo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      line-height: 1.5;
      margin: 20px;
      counter-reset: note section; /* Initialize note + section counters */
    }

    h2 {
      margin-top: 2em;
      counter-increment: section;     /* Increase section count */
      counter-reset: paragraph;       /* Reset paragraph count inside each section */
    }

    p {
      counter-increment: paragraph;   /* Count paragraphs per section */
    }

    /* 1️⃣ List Styles */
    .list-styles ul {
      list-style-type: square;
    }
    .list-styles ol {
      list-style-type: upper-roman;
    }

    /* 2️⃣ Custom counter (footnotes) */
    a.footnote {
      color: blue;
      text-decoration: none;
      counter-increment: note;
    }
    a.footnote::after {
      content: "[S" counter(section) "P" counter(paragraph) "N" counter(note) "]";
      font-size: 0.8em;
      vertical-align: super;
      color: crimson;
    }

    /* 3️⃣ Nested counters */
    .nested li::marker {
      content: counters(list-item, ".") " ";
      font-weight: bold;
    }

    /* 4️⃣ Reversed counters */
    .reversed {
      list-style-type: decimal;
    }
  </style>
</head>
<body>

  <h1>🔢 CSS Counters & List Styles Examples</h1>

  <!-- 1️⃣ List Styles -->
  <h2>1. List Styles</h2>
  <ul class="list-styles">
    <li>Unordered item</li>
    <li>Another item</li>
  </ul>

  <ol class="list-styles">
    <li>First (Roman numeral)</li>
    <li>Second</li>
    <li>Third</li>
  </ol>

  <!-- 2️⃣ Custom Counter -->
  <h2>2. Custom Counter (Footnotes)</h2>
  <p>
    Section with a footnote
    <a href="#" class="footnote">example</a>.
  </p>
  <p>
    Another paragraph with a footnote
    <a href="#" class="footnote">second one</a>.
  </p>

  <!-- 3️⃣ Nested Counters -->
  <h2>3. Nested Counters</h2>
  <ol class="nested">
    <li>Item 1
      <ol>
        <li>Subitem 1</li>
        <li>Subitem 2</li>
      </ol>
    </li>
    <li>Item 2
      <ol>
        <li>Subitem 1</li>
        <li>Subitem 2</li>
      </ol>
    </li>
  </ol>

  <!-- 4️⃣ Reversed Counters -->
  <h2>4. Reversed Counters</h2>
  <ol class="reversed" reversed>
    <li>Step Three</li>
    <li>Step Two</li>
    <li>Step One</li>
  </ol>

  <!-- 5️⃣ Multiple Coun


```
</details>

<img width="632" height="709" alt="image" src="https://github.com/user-attachments/assets/e3195619-6f7b-4e9b-ad9a-db888cdea2e4" />

<img width="260" height="130" alt="image" src="https://github.com/user-attachments/assets/d079a082-f275-4c73-a41b-0811a12b75b8" />

