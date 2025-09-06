

# 🔹 Hidden Features: WeakRef & FinalizationRegistry

## 1. Strong vs Weak References

* **Strong reference** → prevents object from being garbage collected.

  ```js
  let user = { name: "John" }; // strong reference
  ```
* **Weak reference** → does **not** prevent garbage collection.

  * If only weak references remain → object may be deleted anytime.

<br>

## 2. WeakRef

* `WeakRef` creates a weak reference to an object.

  ```js
  let user = { name: "John" };
  let admin = new WeakRef(user); // weak reference
  user = null; // object may now be collected
  ```
* Access via `deref()`:

  ```js
  let ref = admin.deref();
  if (ref) console.log(ref.name); // "John" (if not GC'd yet)
  else console.log("Collected");
  ```

### ⚠️ Notes

* Weak references are **unreliable** → object may or may not exist when dereferenced.
* Should be **avoided unless necessary** (use with care).

<br>

## 3. Use Cases for WeakRef

* **Caching heavy objects** (e.g., images, ArrayBuffer, Blob).
* Prevents cache from “pinning” objects in memory.

  ```js
  let cache = new Map();
  cache.set("img1", new WeakRef(img));
  ```
* **Tracking DOM elements**:

  * Hold weak reference to element.
  * When element removed from DOM → GC cleans it → logger stops.

<br>

## 4. Problem with WeakRef-only Caches

* Keys in `Map` remain even if values are GC’d → “memory leak” of keys.
* Solution → use `FinalizationRegistry` for cleanup.

<br>

## 5. FinalizationRegistry

* Lets you register **cleanup callbacks** (finalizers) when object is GC’d.

  ```js
  const registry = new FinalizationRegistry((heldValue) => {
    console.log(`${heldValue} collected`);
  });

  let user = { name: "John" };
  registry.register(user, user.name);
  ```
* **Methods**:

  * `register(target, heldValue, [unregisterToken])` → track object.
  * `unregister(unregisterToken)` → stop tracking.

### ⚠️ Notes

* Cleanup callback execution is **not guaranteed**:

  * Program exit
  * Registry itself GC’d

<br>

## 6. WeakRef + FinalizationRegistry Together

* Combine for **auto-cleaning caches**.
* Example pattern:

  ```js
  const registry = new FinalizationRegistry((key) => {
    if (!cache.get(key)?.deref()) cache.delete(key);
  });

  cache.set(key, new WeakRef(obj));
  registry.register(obj, key);
  ```
* Benefits:

  * Cache only stores **live entries**.
  * Dead references auto-removed.

<br>

## 7. Real-World Example

* **Photo service cache** (Google Photos/iCloud-like):

  * Thumbnails stored compressed.
  * Full-size images loaded on demand.
  * WeakRef cache prevents excessive memory usage.
  * If GC removes image → fetch again.
* ✅ Saves memory & network requests.
* ❌ Not predictable → GC behavior varies by runtime.

<br>

## 8. Summary

* **WeakRef** → weak reference to object, allows GC to collect it.
* **FinalizationRegistry** → register cleanup callbacks for objects when collected.
* **Use cases**: caches, DOM tracking, memory optimization.
* **Not recommended** for most apps → unpredictable, GC-dependent.
* Better to use **manual cache management** unless memory optimization is critical.
