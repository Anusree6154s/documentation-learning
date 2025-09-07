

## 🔹 File Object

* `File` **inherits from** `Blob`.
* Extra properties:

  * `name` → filename string.
  * `lastModified` → timestamp (last modified).
* Create manually:

  ```js
  new File(parts, name, { lastModified })
  ```
* Usually obtained via:

  * `<input type="file">` (`input.files`).
  * Drag & Drop.
  * Other browser APIs.
* `input.files` → array-like, can hold multiple files.

<br>

## 🔹 FileReader

* Purpose: **read data** from `Blob` / `File`.
* Constructor:

  ```js
  let reader = new FileReader();
  ```

### Methods

* `readAsArrayBuffer(blob)` → binary `ArrayBuffer`.
* `readAsText(blob, [encoding])` → text string.
* `readAsDataURL(blob)` → base64 data URL.
* `abort()` → cancel reading.

### Events

* `loadstart` → reading begins.
* `progress` → during reading.
* `load` → reading finished successfully.
* `abort` → aborted.
* `error` → error occurred.
* `loadend` → finished (success or error).

### Results

* `reader.result` → data after success.
* `reader.error` → error object if failed.

<br>

## 🔹 Usage Example

```html
<input type="file" onchange="readFile(this)">
<script>
  function readFile(input) {
    let file = input.files[0];
    let reader = new FileReader();

    reader.readAsText(file);

    reader.onload = () => console.log(reader.result);
    reader.onerror = () => console.error(reader.error);
  }
</script>
```

<br>

## 🔹 FileReader with Blobs

* Can also read any `Blob`.
* Conversion options:

  * To `ArrayBuffer`.
  * To `string` (`readAsText`).
  * To `base64` (`readAsDataURL`).

<br>

## 🔹 FileReaderSync (Workers only)

* Synchronous version → available **only inside Web Workers**.
* Methods return results directly (no events).
* Doesn’t block UI thread.

<br>

## 🔹 Summary

* `File` = `Blob` + `name` + `lastModified`.
* Sources: `<input type="file">`, drag’n’drop, APIs.
* `FileReader` reads as:

  1. Text.
  2. ArrayBuffer.
  3. Base64 Data URL.
* For displaying files: use `URL.createObjectURL(file)` (no need to read).
* Network APIs (`fetch`, `XHR`) accept `File` directly.
