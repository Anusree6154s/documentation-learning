
## 🔹 URL Object Basics
- `new URL(url, [base])` → creates a URL object.  
- `base` is optional; if given, `url` can be relative.  
- Example:  
  ```js
  new URL('/profile/admin', 'https://javascript.info');
  // → https://javascript.info/profile/admin
  ```  
- Useful for parsing + manipulating URLs.  
- Strings are usually enough, but URL object = **clean parsing + encoding**.

<br>

## 🔹 URL Components (properties)
- `href` → full URL (string).  
- `protocol` → scheme + `:` (e.g. `https:`).  
- `host` → hostname + port.  
- `hostname` → hostname only.  
- `port` → port only.  
- `pathname` → path after domain.  
- `search` → query string (with `?`).  
- `hash` → fragment (with `#`).  
- `username`, `password` → HTTP auth (rare).  

<br>

## 🔹 URLSearchParams
- Access via `url.searchParams`.  
- Methods:  
  - `append(name, value)`  
  - `delete(name)`  
  - `get(name)` / `getAll(name)`  
  - `has(name)`  
  - `set(name, value)`  
  - `sort()`  
- Iterable → works with `for...of`.  
- Handles **auto-encoding**.  
- Example:  
  ```js
  let url = new URL("https://google.com/search");
  url.searchParams.set("q", "test me!");
  console.log(url.toString());
  // https://google.com/search?q=test+me%21
  ```

<br>

## 🔹 Encoding
- RFC3986 defines valid URL chars.  
- URL object auto-encodes invalid ones.  
- Cyrillic/Unicode → converted to `%xx` form.  

<br>

## 🔹 encodeURI vs encodeURIComponent
- **encodeURI** → encodes only forbidden chars (keeps `:,?,=,&,#` intact).  
  - Use for **full URL**.  
- **encodeURIComponent** → encodes forbidden + reserved chars (`#,&,=,?` etc).  
  - Use for **query parameters**.  

✅ Example:  
```js
encodeURIComponent("Rock&Roll"); 
// Rock%26Roll  ✅ safe for query param
encodeURI("http://site.com/привет");
// http://site.com/%D0%BF%D1%80%D0%B8%D0%B2%D0%B5%D1%82
```

<br>

## 🔹 Spec Difference
- URL & URLSearchParams → based on **RFC3986** (latest).  
- encode* functions → based on **RFC2396** (old).  
- Example: IPv6 `http://[2607:f8b0::1007]/` →  
  - `encodeURI` wrongly encodes brackets.  
  - `new URL()` handles correctly.  

<br>

## 🔹 Summary
- `URL` → great for parsing + constructing valid URLs.  
- `URLSearchParams` → easy query param handling.  
- `encodeURI` → whole URL.  
- `encodeURIComponent` → query param (safer for name/value).  
- URL object auto-encodes → more reliable than encode*.  
