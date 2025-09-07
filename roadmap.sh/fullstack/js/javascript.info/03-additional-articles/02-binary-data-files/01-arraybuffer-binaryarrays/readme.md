

### 1. Core Concept

* **`ArrayBuffer`** = raw, fixed-length binary memory.
* Not an array, just a sequence of bytes.
* To access/modify → need a **view**.

<br>

### 2. Views

* **TypedArray** → interprets buffer in a uniform way.

  * `Uint8Array`, `Uint16Array`, `Uint32Array` → unsigned integers.
  * `Int8Array`, `Int16Array`, `Int32Array` → signed integers.
  * `Float32Array`, `Float64Array` → floats.
  * `Uint8ClampedArray` → clamps values (useful for image processing).
* **DataView** → flexible, lets you pick format per access (`getUint8`, `getInt16`, `getFloat32`, …).

<br>

### 3. TypedArray Creation (5 forms)

```js
new TypedArray(buffer, [byteOffset], [length]); // view on buffer
new TypedArray(object); // from array-like, copy values
new TypedArray(typedArray); // from another typed array
new TypedArray(length); // fixed length, zero-filled
new TypedArray(); // empty
```

<br>

### 4. TypedArray Properties

* `length` → number of elements.
* `byteLength` → size in bytes.
* `BYTES_PER_ELEMENT` → element size.
* `buffer` → underlying `ArrayBuffer`.

<br>

### 5. Behavior

* **Out-of-bounds values**: truncated to fit (modulo 2^bits).

  * `Uint8Array([256]) → [0]`.
  * `Uint8Array([257]) → [1]`.
* **`Uint8ClampedArray`**: clamps instead of truncating ( >255 → 255, <0 → 0).

<br>

### 6. Methods

* Supports most array methods (`map`, `forEach`, `slice`, `reduce`, …).
* No `splice` / `concat` (fixed memory).
* Extra:

  * `set(fromArr, offset)` → bulk copy into array.
  * `subarray(begin, end)` → new view, same memory (no copy).

<br>

### 7. DataView

* Constructor:

  ```js
  new DataView(buffer, [byteOffset], [byteLength])
  ```
* Access methods: `getUint8`, `getInt16`, `getFloat32`, `setUint32`, etc.
* Useful for **mixed-format data** in same buffer.

<br>

### 8. Terminology

* **TypedArray** → all typed views.
* **ArrayBufferView** → any view (TypedArray or DataView).
* **BufferSource** → `ArrayBuffer` OR any view.

<br>

### 9. Usage

* File handling, network protocols, image/audio/video processing.
* Efficient binary manipulation.

<br>

✅ **Cheatsheet summary**:

* `ArrayBuffer` = raw memory.
* **TypedArray** = fixed-format view.
* **DataView** = flexible-format view.
* `BufferSource` = either buffer or view.
