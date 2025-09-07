
# ⬇️ Fetch: Download Progress

### 🔹 Key Points

* `fetch` can track **download progress**, but **not upload progress** (for that use `XMLHttpRequest`).
* Progress is tracked using `response.body`, which is a **ReadableStream**.
* Unlike `response.json()` or `response.text()`, using a reader gives **full control** over chunks.

<br>

### 🔹 Reading a Stream

* Get a stream reader:

  ```js
  const reader = response.body.getReader();
  ```
* Reading loop:

  ```js
  while(true) {
    const {done, value} = await reader.read();
    if (done) break;
    console.log(`Received ${value.length} bytes`);
  }
  ```
* Each `value` is a **Uint8Array (chunk of bytes)**.
* `done` = `true` → stream finished.

<br>

### 🔹 Example Flow

1. **Start fetch** and create reader.
2. **Get total size** from `Content-Length` header (may be missing).
3. **Read chunks in loop**, count received bytes, log progress.
4. **Concatenate chunks** into a single `Uint8Array`:

   * Create array of total size.
   * Copy each chunk into it with `.set(chunk, position)`.
5. **Decode result** into string:

   ```js
   let result = new TextDecoder("utf-8").decode(chunksAll);
   let data = JSON.parse(result);
   ```
6. If binary is needed → skip decoding and just:

   ```js
   let blob = new Blob(chunks);
   ```

<br>

### 🔹 Notes & Limitations

* Can’t use both `reader` and `response.json()/text()` → must choose one.
* **Upload progress tracking** is not supported in `fetch`.
* Content-Length may be missing (e.g., cross-origin or streaming).
* Must store chunks during download (can’t “re-read” stream later).
* If size unknown, stop after a safe byte limit to avoid memory issues.
