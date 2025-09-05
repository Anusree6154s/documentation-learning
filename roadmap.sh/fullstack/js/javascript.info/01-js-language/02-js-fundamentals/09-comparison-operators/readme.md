Here’s the content broken down into **clear bullet points** for quick understanding:

---

## **Comparison Operators in JavaScript**

### **Basics**

* `>` , `<` → greater / less
* `>=` , `<=` → greater/less or equal
* `==` → equality (with type conversion)
* `!=` → not equal (with type conversion)
* `===` → strict equality (no type conversion)
* `!==` → strict inequality

---

### **Boolean Results**

* All comparisons return `true` or `false`.

  ```js
  2 > 1   // true
  2 == 1  // false
  2 != 1  // true
  ```

---

### **String Comparison**

* Compared letter-by-letter in Unicode order.
* Example:

  ```js
  "Z" > "A"   // true
  "Glow" > "Glee" // true
  "Bee" > "Be"    // true
  ```
* Case matters: `"a" > "A"` is true because lowercase has a higher Unicode value.

---

### **Different Types**

* Converted to numbers before comparison (except with `===`).

  ```js
  "2" > 1    // true
  "01" == 1  // true
  true == 1  // true
  false == 0 // true
  ```

---

### **Strict Equality**

* <mark>`==` allows type conversion → can cause quirks.</mark>
* <mark>`===` compares both **value** and **type**.</mark>

  ```js
  0 == false   // true
  0 === false  // false
  ```

---

### **null & undefined**

* `null === undefined` → false
* `null == undefined` → true
* In numeric comparisons, `null → 0`, `undefined → NaN`.

  ```js
  null > 0    // false
  null == 0   // false
  null >= 0   // true
  undefined > 0 // false
  undefined < 0 // false
  undefined == 0 // false
  ```

---

### **Safe Practice**

* Avoid comparing values with `null`/`undefined` unless checking with `===`.
* Always handle `null`/`undefined` separately.

---

## **Tasks – What’s the result?**

1. `5 > 4` → **true**
2. `"apple" > "pineapple"` → **false** (comparison stops at `"a"` < `"p"`)
3. `"2" > "12"` → **true** (`"2"` > `"1"` in lexicographic order)
4. `undefined == null` → **true** (special rule)
5. `undefined === null` → **false** (different types)
6. `null == "\n0\n"` → **false** (`"\n0\n"` → 0, `null` only equals `undefined`)
7. `null === +"\n0\n"` → **false** (`+"\n0\n"` → 0, but types differ)