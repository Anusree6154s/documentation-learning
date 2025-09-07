
## 🔹 Basics

* **WebSocket** (RFC 6455) → persistent full-duplex connection between browser & server.
* Suitable for **real-time apps** (chat, games, trading).
* Protocols:

  * `ws://` → unencrypted.
  * `wss://` → encrypted (like HTTPS, preferred & more reliable).

<br>

## 🔹 Lifecycle Events

* `open` → connection established.
* `message` → data received.
* `error` → error occurred.
* `close` → connection closed.

<br>

## 🔹 Usage Example

```js
let socket = new WebSocket("wss://example.com");

socket.onopen = () => socket.send("Hello Server");
socket.onmessage = e => console.log("Received:", e.data);
socket.onclose = e => console.log("Closed:", e.code, e.reason);
socket.onerror = err => console.error("Error:", err);
```

<br>

## 🔹 Handshake

* Starts as **HTTP request**, then upgrades:

  * `Connection: Upgrade`
  * `Upgrade: websocket`
  * `Sec-WebSocket-Key` → random key for verification.
* Server replies with:

  * **101 Switching Protocols** + `Sec-WebSocket-Accept`.
* After that → pure WebSocket protocol (not HTTP).

<br>

## 🔹 Extensions & Subprotocols

* `Sec-WebSocket-Extensions` → e.g., compression.
* `Sec-WebSocket-Protocol` → higher-level formats (e.g., SOAP, WAMP).
* Example:

  ```js
  let socket = new WebSocket("wss://example.com", ["soap", "wamp"]);
  ```

<br>

## 🔹 Data Transfer

* **Frames**:

  * Text frames (string).
  * Binary frames (ArrayBuffer, Blob).
  * Ping/Pong frames (keepalive).
  * Close frame.
* Send:

  ```js
  socket.send("Hello");
  socket.send(new Blob(...));
  ```
* Receive:

  * Text → string.
  * Binary → Blob (default) or ArrayBuffer if `socket.binaryType = "arraybuffer"`.

<br>

## 🔹 Rate Limiting

* `socket.bufferedAmount` → bytes queued for sending.
* Can throttle sending to avoid memory growth.

<br>

## 🔹 Closing Connection

* `socket.close([code], [reason])`
* Codes:

  * `1000` → normal close.
  * `1001` → going away.
  * `1006` → abnormal close (cannot be set manually).
  * `1009` → message too big.
  * `1011` → server error.
* Example:

  ```js
  socket.close(1000, "Done");
  ```

<br>

## 🔹 Connection States (`socket.readyState`)

* `0` → CONNECTING
* `1` → OPEN
* `2` → CLOSING
* `3` → CLOSED

<br>

## 🔹 Example: Chat App

* Client: form sends `socket.send(msg)`, server broadcasts to all clients.
* Server (Node.js with `ws`):

  * Maintain set of clients.
  * On `message` → broadcast.
  * On `close` → remove from set.

<br>

## ✅ Summary

* WebSockets = persistent, bidirectional communication.
* Works cross-origin (no CORS).
* Simple API:

  * Methods → `send()`, `close()`.
  * Events → `open`, `message`, `error`, `close`.
* Supports text & binary.
* Useful for **real-time interactive applications**.
* Needs extra handling for reconnection, auth, scaling.
