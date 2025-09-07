
### 1. Basics
- **EventSource** → built-in class for receiving **server → client** messages.  
- Persistent connection, similar to WebSocket but **one-directional** (server → client only).  
- Uses **HTTP (text/event-stream)**, not a new protocol.  
- Simpler than WebSocket, includes **auto-reconnect**.  

<br>

### 2. EventSource vs WebSocket
| Feature | WebSocket | EventSource |
|---------|-----------|-------------|
| Direction | Bi-directional | Server → Client only |
| Data | Binary + Text | Text only |
| Protocol | WebSocket protocol | Regular HTTP |
| Reconnect | Manual | Automatic |

<br>

### 3. Usage
```js
let eventSource = new EventSource("/events");

eventSource.onmessage = (event) => console.log(event.data);
eventSource.addEventListener("custom", (e) => console.log("Custom:", e.data));
```

<br>

### 4. Server Response Format
- Must send header: `Content-Type: text/event-stream`.  
- Messages separated by `\n\n`.  
- Fields:  
  - `data:` → message body (multiple `data:` lines joined with `\n`).  
  - `id:` → message id, stored in `lastEventId`, sent back as `Last-Event-ID` on reconnect.  
  - `retry:` → reconnection delay (ms).  
  - `event:` → custom event name.  

**Example:**
```
data: Hello
id: 1

event: join
data: Bob
```

<br>

### 5. Connection & Reconnect
- Browser auto-reconnects if connection breaks.  
- Default retry delay = a few seconds (configurable with `retry:`).  
- Server can stop reconnecting → respond with `HTTP 204`.  
- Client can stop reconnecting → `eventSource.close()`.  

<br>

### 6. Cross-Origin
- Supports cross-origin like `fetch`.  
- Browser sends **Origin** header.  
- Server must allow with `Access-Control-Allow-Origin`.  
- To include cookies/credentials:  
```js
let source = new EventSource("https://other.com/events", { withCredentials: true });
```
- Server must also send `Access-Control-Allow-Credentials: true`.  

<br>

### 7. Properties
- `eventSource.readyState`:  
  - `0` = CONNECTING  
  - `1` = OPEN  
  - `2` = CLOSED  
- `eventSource.lastEventId`: last received message id.  

<br>

### 8. Events
- **Built-in:**  
  - `message` → new message (`event.data`).  
  - `open` → connection established.  
  - `error` → connection lost/fatal error.  
- **Custom events**: use `event:` on server + `addEventListener` on client.  

<br>

### 9. Summary
- SSE is ideal for **live updates** (chat, stock prices, notifications).  
- Pros: simple, HTTP-based, auto-reconnect, built-in resume with `Last-Event-ID`.  
- Cons: one-way, text-only, no IE support.  
