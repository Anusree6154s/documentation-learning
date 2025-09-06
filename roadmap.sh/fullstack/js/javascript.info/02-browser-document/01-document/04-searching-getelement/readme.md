
### DOM Searching Methods

#### 🔹 `getElementById(id)`

* Finds an element by its **unique `id`**, anywhere in the document.
* Can only be called on `document` (not on elements).
* The `id` must be **unique**.
* Creates a **global variable with the same name as the id** (not recommended, may cause conflicts).

<br>

#### 🔹 `querySelector(css)`

* Finds the **first** element matching the CSS selector.
* Can be called on `document` or any element.
* Returns **one element** (or `null` if none).
* Faster when you only need the first match.

#### 🔹 `querySelectorAll(css)`

* Finds **all** elements matching the CSS selector.
* Returns a **static NodeList** (does not auto-update).
* Can use **any CSS selector** (including pseudo-classes like `:hover`).

<br>

#### 🔹 `matches(css)`

* Checks if an element matches a given CSS selector.
* Returns `true` / `false`.
* Useful when filtering collections.

<br>

#### 🔹 `closest(css)`

* Finds the **nearest ancestor** (including the element itself) that matches the selector.
* Walks upward through parents until found, or returns `null`.

<br>

### Older `getElementsBy*` Methods (live collections)

#### 🔹 `getElementsByTagName(tag)`

* Returns all elements with the given tag.
* `"*"` finds all tags.
* **Live collection** (updates automatically when DOM changes).

#### 🔹 `getElementsByClassName(class)`

* Returns elements with the given CSS class.
* **Live collection**.

#### 🔹 `getElementsByName(name)`

* Finds elements by their `name` attribute.
* Document-wide search.
* **Rarely used** (mainly for forms).
* **Live collection**.

<br>

### Important Notes

* `getElementById` → single element.
* `getElementsBy*` → multiple elements, **live collections**.
* `querySelector*` → modern choice, **static NodeLists**.
* Don’t forget the **"s"** in `getElementsBy...` (common beginner mistake).
* To modify multiple elements, **iterate over the collection** (not directly assign).

<br>

### Quick Summary Table

| Method                   | Search by    | Can call on element? | Live? |
| ------------------------ | ------------ | -------------------- | ----- |
| `querySelector`          | CSS selector | ✔                    | ✘     |
| `querySelectorAll`       | CSS selector | ✔                    | ✘     |
| `getElementById`         | `id`         | ✘                    | ✘     |
| `getElementsByName`      | `name`       | ✘                    | ✔     |
| `getElementsByTagName`   | Tag or `*`   | ✔                    | ✔     |
| `getElementsByClassName` | Class        | ✔                    | ✔     |

<br>

👉 By far the **most used today** are `querySelector` and `querySelectorAll`.
The `getElementsBy*` methods are mainly **legacy**, but still useful in some cases.
