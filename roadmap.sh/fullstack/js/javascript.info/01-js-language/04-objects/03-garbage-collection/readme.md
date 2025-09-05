

## 📌 Garbage Collection in JavaScript

### 1. Automatic Memory Management

* JavaScript manages memory **automatically**.
* Developers don’t manually allocate/free memory.

<br>

### 2. Key Concept: **Reachability**

* **Reachable = still usable → kept in memory.**
* **Roots (always reachable):**

  * Current executing function + local vars.
  * Other active functions in call stack.
  * Global variables.
* Objects are reachable if they are linked from roots (directly or via references).
* Unreachable = garbage → memory freed.

<br>

### 3. Examples

* **Simple reference**

  ```js
  let user = { name: "John" };
  user = null; // John is unreachable → collected
  ```
* **Two references**

  ```js
  let user = { name: "John" };
  let admin = user;
  user = null; // still reachable via admin
  ```
* **Interlinked objects**

  * Objects can reference each other (e.g., husband-wife).
  * If root reference is deleted, the whole group becomes unreachable → collected.

<br>

### 4. Unreachable Island

* A group of objects referencing each other but not connected to any root → removed.

<br>

### 5. Algorithm: **Mark-and-Sweep**

1. Start from roots → mark them.
2. Follow references → mark reachable objects.
3. Repeat until all reachable are marked.
4. Remove all unmarked (unreachable) objects.
   👉 Think of it as “pouring paint” from roots.

<br>

### 6. Optimizations in Modern Engines

* **Generational collection** → Separate “new” (short-lived) and “old” (long-lived) objects.
* **Incremental collection** → Run GC in small steps instead of all at once.
* **Idle-time collection** → Run GC when CPU is idle.

<br>

### 7. Important Notes

* GC is **automatic** → can’t force or stop it.
* **Referenced ≠ reachable** (a group may reference each other but still be unreachable from roots).
* Advanced GC algorithms differ across engines (e.g., V8, SpiderMonkey).

<br>

✅ **Summary:**

* Memory is freed when objects become **unreachable from roots**.
* Garbage Collection = automatic + optimized.
* Developers just need to understand **reachability**, not manage memory manually.
