

# 🛡️ Clickjacking Attack

### 🔹 Concept

* Trick a user into clicking on a **victim site** without knowing.
* Often done by placing a **transparent iframe** of the victim site over a visible element on the attacker’s page.
* User thinks they click a harmless link/button, but actually interacts with the iframe.

<br>

### 🔹 How It Works (Example with Facebook)

1. User visits attacker’s page.
2. Attacker shows a visible link/button (“Click here to win!”).
3. A **transparent iframe** with Facebook’s Like button is positioned over it using **CSS** (`z-index`, `opacity:0`).
4. Clicking the visible button actually clicks the hidden button inside the iframe.
5. Result: action occurs on victim site (Like, Follow, etc.) using the logged-in session.

<br>

### 🔹 Key Points

* **Clickjacking affects mouse/tap actions**, not keyboard.
* Old-style defense: **framebusting JS**

  ```js
  if (top !== window) top.location = window.location;
  ```

  * Not reliable; can be bypassed.
* Attacker can **block top-navigation** using `beforeunload`.

<br>

### 🔹 Modern Defenses

1. **sandbox attribute on iframe**

   * Restricts navigation, scripts, and forms.
   * Example:

     ```html
     <iframe sandbox="allow-scripts allow-forms" src="victim.html"></iframe>
     ```

2. **X-Frame-Options HTTP header**

   * `DENY` → never allow framing
   * `SAMEORIGIN` → only allow same-origin framing
   * `ALLOW-FROM domain` → allow a specific domain
   * Must be **HTTP header**, not `<meta>` tag.

3. **Overlay <div> (“protector”)**

   * Covers page to intercept clicks.
   * Removed only if page is top-level or safe to interact with.
   * Example:

     ```html
     <div id="protector"></div>
     <script>
       if (top.document.domain == document.domain) protector.remove();
     </script>
     ```

4. **SameSite cookie attribute**

   * Prevents cookies from being sent when page is in a third-party iframe.
   * Stops attacks relying on authenticated sessions.

<br>

### 🔹 Summary

* Clickjacking = tricking user clicks to perform unintended actions.
* Dangerous for **authenticated actions**, voting, likes, transactions.
* Defenses:

  * `X-Frame-Options: SAMEORIGIN`
  * Overlay divs or content blockers
  * `sandbox` iframe restrictions
  * `SameSite` cookies for session protection
