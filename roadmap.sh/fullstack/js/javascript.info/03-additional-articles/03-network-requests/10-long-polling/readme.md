

# 🔄 Long Polling

### 🔹 Regular Polling (baseline)

* Client sends requests at **fixed intervals** (e.g., every 10s):
  *“Hi server, any new messages?”*
* Server replies with any messages received so far.
* **Problems**:

  * Delay up to interval time (e.g., 10s).
  * Wasteful: requests sent even when no messages.
  * Creates **unnecessary load** on server.

<br>

### 🔹 Long Polling (improved)

* **Steps**:

  1. Client sends a request.
  2. Server **holds connection open** until a message is available.
  3. When message appears → server responds.
  4. Client immediately sends a **new request**.
* If connection drops (timeout, error, etc.) → client reconnects.
* This ensures **real-time delivery** without constant empty requests.

<br>

### 🔹 Example Client Code

```js
async function subscribe() {
  let response = await fetch("/subscribe");

  if (response.status == 502) {
    // connection timeout → retry
    await subscribe();
  } else if (response.status != 200) {
    showMessage(response.statusText);
    await new Promise(resolve => setTimeout(resolve, 1000));
    await subscribe();
  } else {
    let message = await response.text();
    showMessage(message);
    await subscribe(); // get next message
  }
}
subscribe();
```

<br>

### 🔹 Server Considerations

* Must handle **many open/pending connections**.
* Some architectures (e.g., PHP, Ruby with one-process-per-connection) may struggle.
* Event-driven servers (e.g., **Node.js**) handle it efficiently.

<br>

### 🔹 Use Cases

* Good for **rare/occasional messages** (chat, notifications, updates).
* If messages are **frequent**, overhead (headers, repeated requests) becomes large → better to use **WebSockets** or **Server-Sent Events (SSE)**.

<br>

⚡ In short:
Long polling = **low-latency message delivery** using **held requests**.
Efficient for **infrequent events**, but heavy for **high-frequency messaging**.
