

## 🔹 Blob Basics

* **Blob** = “binary large object” → binary data with **type** (MIME).
* Defined in **File API** (browser feature).
* Constructor:

  ```js
  new Blob(blobParts, options)
  ```

  * `blobParts`: array of `Blob`, `BufferSource`, or `String`.
  * `options`:

    * `type`: MIME type (e.g. `"image/png"`, `"text/html"`).
    * `endings`: newline handling → `"transparent"` (default) or `"native"`.

<br>

## 🔹 Creating Blobs

* From string:

  ```js
  new Blob(["<html>…</html>"], {type: "text/html"})
  ```
* From binary + string:

  ```js
  let hello = new Uint8Array([72,101,108,108,111]);
  new Blob([hello, " ", "world"], {type: "text/plain"});
  ```

<br>

## 🔹 Blob Properties

* Immutable → can’t modify directly.
* Can create **slices**:

  ```js
  blob.slice(byteStart, byteEnd, contentType);
  ```
* Behaves like strings → new blob must be created for changes.

<br>

## 🔹 Blob as URL

* `URL.createObjectURL(blob)` → generates a short-lived blob URL:
  `blob:<origin>/<uuid>`
* Example:

  ```js
  let blob = new Blob(["Hello!"], {type: "text/plain"});
  link.href = URL.createObjectURL(blob);
  ```
* Must call `URL.revokeObjectURL(url)` when done → free memory.
* Valid only in current document.

<br>

## 🔹 Blob as Base64

* Use `FileReader`:

  ```js
  let reader = new FileReader();
  reader.readAsDataURL(blob);
  reader.onload = () => link.href = reader.result;
  ```
* Produces `data:[type];base64,...` string.
* Pros: no cleanup needed.
* Cons: slower, more memory (especially for large Blobs).

<br>

## 🔹 Blob with Canvas

* Create Blob of images/screenshots:

  ```js
  canvas.toBlob(blob => {
    let url = URL.createObjectURL(blob);
  }, "image/png");
  ```
* Useful for editing/cropping images.

<br>

## 🔹 Conversion with ArrayBuffer

* Blob → ArrayBuffer:

  ```js
  let buffer = await blob.arrayBuffer();
  ```
* Good for **low-level binary processing**.

<br>

## 🔹 Blob as Stream

* For **large files (>2GB)**:

  ```js
  const reader = blob.stream().getReader();
  while (true) {
    let {done, value} = await reader.read();
    if (done) break;
    console.log(value);
  }
  ```
* Allows processing piece by piece → avoids memory overload.

<br>

## 🔹 Summary

* **ArrayBuffer / TypedArray** → raw binary.
* **Blob** → binary with type (better for upload/download).
* **URL.createObjectURL(blob)** → best for quick usage (needs revoking).
* **FileReader.readAsDataURL(blob)** → converts to base64 (heavier).
* **Canvas.toBlob()** → create image blobs.
* **blob.arrayBuffer() / blob.stream()** → convert to raw binary or stream for large data.
