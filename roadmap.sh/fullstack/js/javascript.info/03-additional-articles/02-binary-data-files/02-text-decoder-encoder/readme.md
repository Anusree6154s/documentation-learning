

## 🔹 TextDecoder

* Converts **binary data** (ArrayBuffer / Uint8Array) into a **JavaScript string**.
* **Syntax:**

  ```js
  let decoder = new TextDecoder([label], [options]);
  ```

  * `label` → encoding, default `"utf-8"` (others: `"big5"`, `"windows-1251"`, etc.)
  * `options` → object:

    * `fatal` (boolean) → throw error on invalid characters (default: false, replaces with `\uFFFD`)
    * `ignoreBOM` (boolean) → ignore BOM mark (rarely needed)
* **Decoding:**

  ```js
  let str = decoder.decode([input], [options]);
  ```

  * `input` → BufferSource to decode
  * `options` → `{ stream: true }` for chunked decoding (handles split multi-byte chars)
* **Examples:**

  ```js
  let uint8Array = new Uint8Array([72,101,108,108,111]);
  new TextDecoder().decode(uint8Array); // "Hello"

  let uint8Array = new Uint8Array([228,189,160,229,165,189]);
  new TextDecoder().decode(uint8Array); // "你好"
  ```
* Can decode **subarrays** of a buffer without copying:

  ```js
  let binaryString = uint8Array.subarray(1, -1);
  new TextDecoder().decode(binaryString); // "Hello"
  ```

<br>

## 🔹 TextEncoder

* Converts a **string** into **bytes (Uint8Array)**.
* **Syntax:**

  ```js
  let encoder = new TextEncoder();
  ```

  * Only supports `"utf-8"` encoding.
* **Methods:**

  * `encode(str)` → returns Uint8Array
  * `encodeInto(str, destination)` → encodes into existing Uint8Array
* **Example:**

  ```js
  let encoder = new TextEncoder();
  let uint8Array = encoder.encode("Hello");
  console.log(uint8Array); // Uint8Array [72, 101, 108, 108, 111]
  ```
