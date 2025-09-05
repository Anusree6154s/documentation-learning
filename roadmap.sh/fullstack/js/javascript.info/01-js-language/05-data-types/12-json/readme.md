

## 🔹 JSON Basics

* **JSON (JavaScript Object Notation)** = text-based format to represent structured data.
* Independent of JavaScript → used across many languages.
* In JS:

  * `JSON.stringify(obj)` → converts object → JSON string.
  * `JSON.parse(str)` → converts JSON string → object.

<br>

## 🔹 JSON.stringify

**Syntax:**

```js
JSON.stringify(value, replacer, space);
```

* **value** → object/value to encode.
* **replacer** (optional) → filter or transform (array of keys or function).
* **space** (optional) → pretty formatting (number of spaces or custom string).

✅ Converts objects, arrays, primitives (`string`, `number`, `boolean`, `null`).
❌ Skips:

* functions
* `undefined`
* symbols

### Examples

```js
JSON.stringify(1);             // "1"
JSON.stringify("test");        // "\"test\""
JSON.stringify([1,2,3]);       // "[1,2,3]"
JSON.stringify({a:1, b:2});    // "{"a":1,"b":2}"
```

<br>

## 🔹 Nested Objects

* Works automatically.

```js
let obj = { user: { name: "John", age: 30 } };
JSON.stringify(obj);
// {"user":{"name":"John","age":30}}
```

❌ **Fails with circular references.**

<br>

## 🔹 Handling Circular References

Use `replacer` to exclude properties.

```js
JSON.stringify(meetup, function(key, value) {
  return (key === "self" || key === "occupiedBy") ? undefined : value;
});
```

<br>

## 🔹 Replacer

1. **As array (whitelist keys):**

```js
JSON.stringify(user, ["name", "age"]);
```

2. **As function:**

```js
JSON.stringify(obj, (key, value) => {
  if (key === "password") return undefined;
  return value;
});
```

<br>

## 🔹 Formatting (space)

```js
JSON.stringify(user, null, 2); // indented with 2 spaces
JSON.stringify(user, null, "♥"); // indented with "♥"
```

<br>

## 🔹 Custom toJSON

* Objects can define a `toJSON()` method.
* Automatically called by `JSON.stringify`.

```js
let room = {
  number: 23,
  toJSON() { return this.number; }
};
JSON.stringify(room); // "23"
```

Dates have built-in `toJSON` → ISO string.

<br>

## 🔹 JSON.parse

**Syntax:**

```js
JSON.parse(str, reviver);
```

* **str** → JSON string to decode.
* **reviver** (optional) → function `(key, value)` to transform values.

### Example:

```js
let str = '{"name":"John","age":30}';
let obj = JSON.parse(str);
console.log(obj.name); // "John"
```

<br>

## 🔹 Reviver

* Allows **post-processing** (e.g., restore Dates).

```js
let str = '{"date":"2023-01-01T00:00:00.000Z"}';
let obj = JSON.parse(str, (key, value) =>
  key === "date" ? new Date(value) : value
);
console.log(obj.date.getFullYear()); // 2023
```

<br>

## ✅ Summary

* `JSON.stringify` → object → JSON string.
* `JSON.parse` → JSON string → object.
* `replacer` (stringify) and `reviver` (parse) allow filtering/transforming.
* `space` adds pretty formatting.
* `toJSON` customizes object serialization.
* **Circular references must be handled** (exclude offending properties).

<br>

⚡ Tasks Recap:

1. **Turn object into JSON and back**

```js
let user = { name: "John Smith", age: 35 };
let json = JSON.stringify(user);
let user2 = JSON.parse(json);
```

2. **Exclude circular references**

```js
JSON.stringify(meetup, function(key, value) {
  return (value === meetup) ? undefined : value;
});
```