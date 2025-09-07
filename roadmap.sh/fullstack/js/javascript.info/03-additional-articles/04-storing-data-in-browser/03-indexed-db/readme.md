
# 📦 IndexedDB — Quick Notes

## 1. Basics
- Browser-built database → more powerful than `localStorage`.  
- Stores almost any values (objects, arrays, binary, dates).  
- Much larger storage limits than `localStorage`.  
- Event-based API (callbacks), but promise wrapper (`idb`) available.  
- Good for **offline apps** (works with Service Workers).  

<br>

## 2. Opening / Versioning
```js
let openReq = indexedDB.open(name, version);
```
Events:
- `success` → DB ready (`openReq.result`).  
- `error` → opening failed.  
- `upgradeneeded` → DB doesn’t exist or needs schema update.  

- Versioning ensures schema evolution.  
- If old JS tries to open lower version → error.  
- Parallel update:  
  - `db.onversionchange` → close old connection.  
  - `openReq.onblocked` → new version blocked by old connection.  

Delete DB → `indexedDB.deleteDatabase(name)`.  

<br>

## 3. Object Store (like “tables”)
- Created in `upgradeneeded`.  
```js
db.createObjectStore("books", { keyPath: "id" });
```
Options:  
- `keyPath`: auto-use object property as key.  
- `autoIncrement`: DB generates numeric keys.  
- Must have unique key for each value.  
- To delete → `db.deleteObjectStore("books")`.  

<br>

## 4. Transactions
```js
let tx = db.transaction("books", "readwrite");
let store = tx.objectStore("books");
```
Types:
- `readonly` (default) → concurrent allowed.  
- `readwrite` → exclusive lock until complete.  
- `versionchange` → only auto (during schema upgrade).  

Auto-commits when all requests finish (⚠️ no `setTimeout/fetch` inside).  
Events: `tx.oncomplete`, `tx.onabort`.  
Abort manually: `tx.abort()`.  

<br>

## 5. Adding / Updating
- `store.add(value, [key])` → fails if key exists.  
- `store.put(value, [key])` → replaces if key exists.  
- Errors auto-abort transaction (prevent with `event.preventDefault()`).  

<br>

## 6. Error Handling
- Errors bubble: request → transaction → db.  
- Can `stopPropagation()` to silence.  
- Example: handle `ConstraintError` for duplicate keys.  

<br>

## 7. Searching
### By Key / Key Range
`IDBKeyRange` helpers:  
- `only(key)` → exact.  
- `lowerBound(val, open)` → `>= val`.  
- `upperBound(val, open)` → `<= val`.  
- `bound(lower, upper, lowerOpen, upperOpen)` → between.  

Methods:  
- `store.get(keyOrRange)`  
- `store.getAll([query], [count])`  
- `store.getKey(query)`  
- `store.getAllKeys([query])`  
- `store.count([query])`  

<br>

## 8. Indexes (search by field)
```js
store.createIndex("price_idx", "price", { unique: false });
```
- Tracks given field automatically.  
- Search via index:  
```js
let idx = store.index("price_idx");
idx.getAll(10);
idx.getAll(IDBKeyRange.upperBound(5));
```
- Results sorted by index key.  

<br>

## 9. Deletion
- By key → `store.delete(key)`.  
- Clear all → `store.clear()`.  
- By field → find with index, then delete by key.  

<br>

## 10. Cursors (for large data)
```js
let req = store.openCursor(query, "next");
req.onsuccess = e => {
  let cursor = req.result;
  if (cursor) { console.log(cursor.key, cursor.value); cursor.continue(); }
};
```
- `advance(n)` → skip ahead.  
- Over index:  
  - `cursor.key` → index field (e.g. price).  
  - `cursor.primaryKey` → actual object key.  

<br>

## 11. Promise Wrapper (`idb`)
```js
let db = await idb.openDB("store", 1, {
  upgrade(db) { db.createObjectStore("books", { keyPath: "id" }); }
});
await db.transaction("books", "readwrite").objectStore("books").add({...});
```
- Cleaner async/await code.  
- ⚠️ Still auto-commit issues with async macrotasks (`fetch`, `setTimeout`).  

<br>

## 12. Summary
- **IndexedDB = localStorage on steroids**.  
- Key features:  
  - Transactions (ACID-like).  
  - Object stores + indexes.  
  - Key ranges + cursors for queries.  
- Best for offline apps needing structured, large data storage.  
