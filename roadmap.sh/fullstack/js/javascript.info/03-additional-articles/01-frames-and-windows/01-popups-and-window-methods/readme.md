

# 🪟 Popups & Window Methods

## 1. Opening a Popup

* `window.open(url, name, params)`

  * **url** → page to load (default: `"about:blank"`)
  * **name** → window name (reuses if exists)
  * **params** → comma-separated features, e.g. `"width=400,height=300,left=100,top=100"`

📌 **Params options**

* `left/top` → screen position
* `width/height` → popup size (min limits apply)
* `menubar, toolbar, location, status, resizable, scrollbars` → yes/no features

<br>

## 2. Popup Blocking

* Browsers block popups if **not triggered by user action** (e.g. in `onclick`).
* Allowed only in **user-triggered handlers**.

<br>

## 3. Popup Behavior

* By default → may open in a **new tab**.
* With size params → opens as a **separate popup window**.
* Browsers may “fix” odd params (e.g. `width=0` → full screen).

<br>

## 4. Accessing Popup & Opener

* `let win = window.open(...);` → reference to popup.
* Can `win.document.write(...)` or modify after `win.onload`.
* **Same-origin policy**:

  * If same origin → both windows can freely read/write.
  * If different origin → only limited actions (e.g. change location, send messages).
* Popup can access opener via `window.opener`.

<br>

## 5. Closing a Popup

* `win.close()` → closes popup (works only if created via `window.open`).
* `win.closed` → `true` if popup already closed.
* Users may close popup manually anytime → always check `.closed`.

<br>

## 6. Moving & Resizing

* `win.moveBy(x, y)` → move relative to current position.
* `win.moveTo(x, y)` → move to absolute screen position.
* `win.resizeBy(w, h)` → resize relative to current size.
* `win.resizeTo(w, h)` → resize to exact size.
  ⚠️ Only works for popups (not tabs, not maximized windows).

<br>

## 7. Scrolling

* `win.scrollBy(x, y)` → scroll relative.
* `win.scrollTo(x, y)` → scroll absolute.
* `elem.scrollIntoView(true/false)` → scroll page until element is visible.
* Event: `window.onscroll`.

<br>

## 8. Focus & Blur

* `win.focus()` → bring popup to front (not always reliable).
* `win.blur()` → unfocus.
* Events: `window.onfocus`, `window.onblur` → detect switching in/out.
  ⚠️ Browsers restrict abuse (e.g. locking user in window).

<br>

## 9. Summary

* Popups are **rarely used** today (replaced by modals/iframes).
* Still useful for **OAuth / auth flows**.
* Always inform user (icon or text: "opens in new window").
* **Best practices**:

  * Open via user action.
  * Provide size/position.
  * Handle popup closure gracefully.
