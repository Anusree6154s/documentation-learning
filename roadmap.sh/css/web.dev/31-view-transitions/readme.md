
### View Transitions for Single Page Applications (SPA)

**1. What are they?**

* SPAs replace DOM content dynamically instead of reloading a page.
* <mark>View transitions show continuity between views (instead of content just “appearing”). Old element is shown for sometime. Something like fade in out</mark>

<br>

**2. Full Page Transitions**

* Default behavior: old view fades out, new view fades in.

```js
document.startViewTransition(() => updateTheDOMSomehow());
```

* **Fallback (no support):**

```js
if (!document.startViewTransition) {
  updateTheDOMSomehow();
} else {
  document.startViewTransition(() => updateTheDOMSomehow());
}
```

<br>

**3. How It Works**

* Browser snapshots old view.
* Callback updates DOM to new view (hidden).
* Transition animates between old + new.

<br>

**4. Customizing Transitions**

* Style pseudo-elements:

  * `::view-transition-old()` → leaving view
  * `::view-transition-new()` → entering view
  * `::view-transition-group()` → both

```css
::view-transition-group(root){
  animation-duration: 200ms;
}
::view-transition-old(root) { animation-name: slide-out-to-left; }
::view-transition-new(root) { animation-name: slide-in-from-right; }
```

<br>

**5. Context-Based Transitions**

* Different transitions for “forward” vs “backward” navigation.

```css
html:active-view-transition-type(forwards) {
  &::view-transition-old(root) { animation-name: slide-out-to-left; }
  &::view-transition-new(root) { animation-name: slide-in-from-right; }
}
```

```js
const direction = next === 'home' ? 'backwards' : 'forwards';
document.startViewTransition({ update: updateTheDOMSomehow, types: [direction] });
```

<br>

**6. Transitioning Specific Elements**

* Use `view-transition-name` on elements present in both old + new view.

```html
<h2 style="view-transition-name: title">Blog Post Title</h2>
<img style="view-transition-name: image" src="thumb.jpg">
```

* Must exist **once in old view + once in new view**.

<br>

**7. Multiple Matches (like blog posts)**

* Option A: Generate unique `view-transition-name` per item (e.g., post ID).
* Option B: Apply a generic name only to the clicked item before transition.

<br>

**8. Designing Smooth Transitions**

* Use `width: fit-content` for text to avoid wrapping changes.
* Adjust `object-fit` for images with different aspect ratios.

<br>

**9. Accessibility: Prefers Reduced Motion**

* Disable or replace transitions for motion-sensitive users.

```css
@media (prefers-reduced-motion) {
  ::view-transition-group(*),
  ::view-transition-old(*),
  ::view-transition-new(*) {
    animation: none !important;
  }
}
```
## Examples
<details>
  <summary>Code</summary>

  ```htl
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>SPA View Transition Demo</title>
    <style>
      body {
        font-family: sans-serif;
        text-align: center;
        padding: 40px;
      }

      /* Buttons */
      button {
        padding: 10px 20px;
        margin: 20px;
        font-size: 1rem;
        cursor: pointer;
        border: none;
        border-radius: 6px;
        background: dodgerblue;
        color: white;
      }

      /* Custom slide animations for root */
      @keyframes slide-out-to-left {
        from {
          transform: translateX(0);
          opacity: 1;
        }
        to {
          transform: translateX(-100%);
          opacity: 0;
        }
      }

      @keyframes slide-in-from-right {
        from {
          transform: translateX(100%);
          opacity: 0;
        }
        to {
          transform: translateX(0);
          opacity: 1;
        }
      }

      ::view-transition-group(root) {
        animation-duration: 400ms;
      }

      ::view-transition-old(root) {
        animation-name: slide-out-to-left;
      }

      ::view-transition-new(root) {
        animation-name: slide-in-from-right;
      }

      /* Transition a specific element (title) */
      h1 {
        view-transition-name: page-title;
      }

      /* Accessibility: disable transitions if user prefers reduced motion */
      @media (prefers-reduced-motion) {
        ::view-transition-group(*),
        ::view-transition-old(*),
        ::view-transition-new(*) {
          animation: none !important;
        }
      }
    </style>
  </head>
  <body>
    <div id="app">
      <h1>Home Page</h1>
      <p>Welcome to the home page! 🚀</p>
      <button id="goPost">Go to Post</button>
    </div>

    <script>
      const app = document.getElementById("app");
      let onHome = true;

      function updateTheDOMSomehow() {
        if (onHome) {
          app.innerHTML = `
          <h1>Blog Post</h1>
          <p>This is a sample blog post with smooth transition. ✨</p>
          <button id="goHome">Back Home</button>
        `;
        } else {
          app.innerHTML = `
          <h1>Home Page</h1>
          <p>Welcome to the home page! 🚀</p>
          <button id="goPost">Go to Post</button>
        `;
        }
        onHome = !onHome;
      }

      // Event delegation for buttons
      document.body.addEventListener("click", (e) => {
        if (e.target.id === "goPost" || e.target.id === "goHome") {
          if (!document.startViewTransition) {
            updateTheDOMSomehow(); // fallback
          } else {
            document.startViewTransition(() => updateTheDOMSomehow());
          }
        }
      });
    </script>
  </body>
</html>

```
</details>


https://github.com/user-attachments/assets/10f8bdbb-d85a-4a99-83a9-4e9888a736cd

