

### 📌 Problem

* With `fetch`, uploading files is simple.
* But **resuming after a lost connection** is not built-in.
* To resume → must know **exactly how many bytes the server already has**.
* Only the **server** can confirm received bytes (progress events in browser are unreliable).

---

### ⚠️ Limitation of `xhr.upload.onprogress`

* Tracks how much data is **sent** by browser.
* Doesn’t guarantee how much was actually **received by server**.
* Useful only for a progress bar, not for resuming uploads.

---

### 🛠️ Algorithm for resumable upload

1. **Generate a unique file ID**

   ```js
   let fileId = file.name + '-' + file.size + '-' + file.lastModified;
   ```

   * Ensures resume works only for the same file.

2. **Ask server how many bytes it already has**

   ```js
   let response = await fetch('status', {
     headers: { 'X-File-Id': fileId }
   });
   let startByte = +await response.text(); // e.g., 0 if new
   ```

3. **Resume upload from that byte** using `Blob.slice`:

   ```js
   xhr.open("POST", "upload");
   xhr.setRequestHeader('X-File-Id', fileId);
   xhr.setRequestHeader('X-Start-Byte', startByte);

   xhr.upload.onprogress = (e) => {
     console.log(`Uploaded ${startByte + e.loaded} of ${startByte + e.total}`);
   };

   xhr.send(file.slice(startByte));
   ```

4. **Server responsibility**:

   * Track uploaded files by `X-File-Id`.
   * Confirm if `X-Start-Byte` matches stored data.
   * If so → append new data to file.

---

### ✅ Summary

* Use `XMLHttpRequest` instead of `fetch` for resumable uploads (progress tracking + partial upload).
* Steps:

  1. Create **file ID**.
  2. Ask server for **uploaded bytes**.
  3. Resume with `file.slice(startByte)`.
  4. Server validates headers (`X-File-Id`, `X-Start-Byte`) and appends data.
