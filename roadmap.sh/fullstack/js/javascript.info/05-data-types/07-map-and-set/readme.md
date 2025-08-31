

## **Map**
- Collection of **key → value** pairs (like Objects, but more powerful).  
- **Key differences from Object**:
  - Keys can be **any type** (including objects, NaN, etc.).  
  - Preserves **insertion order**.  
- **Methods & properties**:  
  - `new Map([iterable])` → create map.  
  - `map.set(key, value)` → add/update entry (returns map, allows chaining).  
  - `map.get(key)` → get value (or `undefined`).  
  - `map.has(key)` → check key existence.  
  - `map.delete(key)` → remove by key.  
  - `map.clear()` → remove all.  
  - `map.size` → count of elements.  
- **Iteration**:  
  - `map.keys()` → iterable of keys.  
  - `map.values()` → iterable of values.  
  - `map.entries()` → iterable of `[key, value]` (default for `for..of`).  
  - `map.forEach((value, key, map) => {...})`.  

<br>

## **Set**
- Collection of **unique values** (no duplicates).  
- **Methods & properties**:  
  - `new Set([iterable])` → create set.  
  - `set.add(value)` → add (ignores duplicates).  
  - `set.has(value)` → check if exists.  
  - `set.delete(value)` → remove value.  
  - `set.clear()` → remove all.  
  - `set.size` → count of unique values.  
- **Iteration**:  
  - `for..of` or `set.forEach`.  
  - `set.keys()`, `set.values()`, `set.entries()` (compatibility with Map).  

<br>

## **Conversions**
- `Object.entries(obj)` → array of `[key, value]` → useful to create `new Map`.  
- `Object.fromEntries(map)` → plain object from Map.  

<br>

## **Tasks & Solutions**

### 1. **Filter unique array members**
```js
function unique(arr) {
  return Array.from(new Set(arr));
}

let values = ["Hare", "Krishna", "Hare", "Krishna",
  "Krishna", "Krishna", "Hare", "Hare", ":-O"
];

alert(unique(values)); // ["Hare", "Krishna", ":-O"]
```

<br>

### 2. **Filter anagrams**
```js
function aclean(arr) {
  let map = new Map();
  for (let word of arr) {
    let sorted = word.toLowerCase().split("").sort().join("");
    map.set(sorted, word); // keep only one per group
  }
  return Array.from(map.values());
}

let arr = ["nap", "teachers", "cheaters", "PAN", "ear", "era", "hectares"];
alert(aclean(arr)); // ["nap", "teachers", "ear"] (order may vary)
```

<br>

### 3. **Iterable keys problem**
```js
let map = new Map();
map.set("name", "John");

let keys = Array.from(map.keys()); // convert iterable to array
keys.push("more");

alert(keys); // ["name", "more"]
```
- Fix: `map.keys()` returns an **iterable**, not an array → use `Array.from()`.

<br>

✅ **Summary**
- **Map** = keyed collection (any type keys, insertion order).  
- **Set** = collection of unique values.  
- Use `Array.from()` to convert map/set iterables into arrays.  
- Both preserve insertion order when iterating.  
