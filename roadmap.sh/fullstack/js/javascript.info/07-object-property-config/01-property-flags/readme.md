

## 🔹 Property Flags

Each object property has 3 special attributes (besides value):

* **writable** → `true` if value can be changed.
* **enumerable** → `true` if property shows up in loops (`for..in`, `Object.keys`).
* **configurable** → `true` if property can be deleted or its flags changed.

Default for normal properties → all `true`.

<br>

## 🔹 Methods

* **`Object.getOwnPropertyDescriptor(obj, prop)`** → returns descriptor of a property.
* **`Object.defineProperty(obj, prop, descriptor)`** → creates/updates property with specific flags.
* **`Object.defineProperties(obj, descriptors)`** → define multiple properties at once.
* **`Object.getOwnPropertyDescriptors(obj)`** → get descriptors of all properties.

<br>

## 🔹 Effects of Flags

1. **Non-writable (`writable: false`)**

   * Value cannot be changed.
   * In strict mode → error.
   * In non-strict mode → silently ignored.

2. **Non-enumerable (`enumerable: false`)**

   * Hidden from `for..in`, `Object.keys`.
   * Example: built-in `toString` is non-enumerable.

3. **Non-configurable (`configurable: false`)**

   * Property cannot be deleted.
   * Flags cannot be changed (except `writable: true → false`).
   * Example: `Math.PI` → non-writable, non-enumerable, non-configurable.

<br>

## 🔹 Object-level Freezing/Sealing

* **`Object.preventExtensions(obj)`** → no new properties allowed.
* **`Object.seal(obj)`** → prevents add/remove, sets all properties `configurable: false`.
* **`Object.freeze(obj)`** → prevents add/remove/change, sets all properties `configurable: false, writable: false`.

<br>

## 🔹 Tests

* **`Object.isExtensible(obj)`** → `false` if no new properties allowed.
* **`Object.isSealed(obj)`** → `true` if add/remove forbidden + all `configurable: false`.
* **`Object.isFrozen(obj)`** → `true` if fully immutable (`configurable: false, writable: false`).

<br>

⚡ In short:

* `writable` → can change value.
* `enumerable` → shows in loops.
* `configurable` → can delete or reconfigure.
* Use **defineProperty / defineProperties** for precise control.
* Use **seal / freeze** for object-wide immutability.
