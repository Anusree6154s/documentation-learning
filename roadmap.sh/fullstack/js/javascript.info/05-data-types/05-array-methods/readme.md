

## 📌 Array Methods Cheat Sheet

### 🔹 Add/Remove Items

* `arr.push(...items)` → add to end
* `arr.pop()` → remove from end
* `arr.shift()` → remove from start
* `arr.unshift(...items)` → add to start
* `arr.splice(start, deleteCount, ...items)` → remove/replace/insert
* `arr.slice(start, end)` → copy portion into new array
* `arr.concat(...items)` → merge arrays/values

<br>

### 🔹 Iteration

* `arr.forEach(fn)` → run function for each item (no return)

<br>

### 🔹 Searching

* `arr.indexOf(value, from)` → index or `-1`
* `arr.lastIndexOf(value, from)` → last index or `-1`
* `arr.includes(value, from)` → true/false (handles `NaN`)
* `arr.find(fn)` → first element matching
* `arr.findIndex(fn)` → index of first match
* `arr.findLastIndex(fn)` → index of last match
* `arr.filter(fn)` → all matches

<br>

### 🔹 Transformation

* `arr.map(fn)` → new array with results
* `arr.sort(fn)` → sort in place (default: string compare)
* `arr.reverse()` → reverse in place
* `str.split(delim)` → string → array
* `arr.join(glue)` → array → string
* `arr.reduce(fn, initial)` → single value (left → right)
* `arr.reduceRight(fn, initial)` → single value (right → left)

<br>

### 🔹 Checks

* `Array.isArray(value)` → true/false
* `arr.some(fn)` → true if any item passes test
* `arr.every(fn)` → true if all items pass test

<br>

### 🔹 Other Useful

* `arr.fill(value, start, end)` → fill with value
* `arr.copyWithin(target, start, end)` → copy within itself
* `arr.flat(depth)` → flatten nested arrays
* `arr.flatMap(fn)` → map + flatten

<br>

## 📌 Practice Tasks (with hints)

1. **Camelize string**
   → `split('-')`, capitalize after dash, `join('')`

2. **Filter range (new array)**
   → `filter(x => a ≤ x ≤ b)`

3. **Filter range in place**
   → loop + `splice`

4. **Sort decreasing**
   → `arr.sort((a,b)=>b-a)`

5. **Copy & sort array**
   → `arr.slice().sort()`

6. **Extendable calculator**
   → class with `calculate(str)` + `addMethod`

7. **Map to names**
   → `users.map(u => u.name)`

8. **Map to objects (fullName + id)**
   → `users.map(u => ({fullName: u.name+" "+u.surname, id: u.id}))`

9. **Sort users by age**
   → `arr.sort((a,b)=>a.age-b.age)`

10. **Shuffle array**
    → Fisher–Yates shuffle

11. **Get average age**
    → `reduce((sum,u)=>sum+u.age,0)/arr.length`

12. **Unique items**
    → `Array.from(new Set(arr))`

13. **Group by id**
    → `reduce((obj,u)=>{obj[u.id]=u; return obj}, {})`
