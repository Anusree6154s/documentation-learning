
### Private and Protected Properties/Methods in JS (Encapsulation)

**Concept**

* Encapsulation = separating **internal interface** (hidden details) from **external interface** (public methods/properties).
* Real-world analogy → Coffee machine: simple buttons outside, complex parts inside.

<br>

### Types of Properties/Methods in JavaScript

1. **Public**

   * Accessible from anywhere.
   * Default in JavaScript.

2. **Protected (convention only)**

   * Start with `_` (underscore).
   * Not enforced by language, but convention: only used inside class or subclasses.
   * Example: `_waterAmount` → use getter/setter to prevent invalid values.

3. **Private (language-enforced)**

   * Start with `#`.
   * Enforced by JS → cannot be accessed outside class or by subclasses.
   * Example: `#waterLimit`, `#fixWaterAmount()`.
   * Unlike protected, not inherited directly.

<br>

### Techniques

* **Getters/Setters**

  * Control property access.
  * Can enforce rules (e.g., prevent negative water).
  * `get`/`set` syntax (shorter) OR explicit `getSomething()`/`setSomething()` methods (more flexible).

* **Read-only properties**

  * Implement with getter only (no setter).
  * Example: `power` in coffee machine.

<br>

### Key Limitations & Rules

* Private fields `#` cannot be accessed via `this[name]`.
* Private fields are **not** inherited by subclasses → must rely on public/protected accessors.
* Protected fields `_` **are** inheritable (by convention).

<br>

### Benefits of Encapsulation

1. **Protection** → Prevents accidental misuse (no “shooting yourself in the foot”).
2. **Supportability** → Internal code can change freely without breaking external use.
3. **Hiding Complexity** → Users get a simple, well-documented interface.

<br>

✅ **Summary:**

* Use **`_` (protected by convention)** when subclasses may need access.
* Use **`#` (private, enforced)** for strict privacy inside a class.
* Encapsulation makes code **safe, maintainable, and user-friendly**.
