
### 🎬 CSS Animations 

**1. What is animation in CSS?**

* Animation = sequence of keyframes over time.
* Can be simple (2 states) or complex (multiple keyframes).
* Runs automatically in the browser, no JavaScript required.

<br>

**2. Keyframes (`@keyframes`)**

* Define animation states at specific points in the timeline.
* Keywords:

  * `from` = 0%
  * `to` = 100%
* Example:

```css
@keyframes pulse {
  0% { opacity: 0; }
  50% { transform: scale(1.4); opacity: 0.4; }
  100% { opacity: 1; }
}
```

<br>

**3. Animation properties**

* **`animation-name`** → reference the keyframes.
* **`animation-duration`** → how long (e.g., `2s`). Default = `0s`.
* **`animation-timing-function`** → controls speed curve.

  * Presets: `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`.
  * Custom: `cubic-bezier(x1, y1, x2, y2)`
  * Steps: `steps(n, start|end)` for discrete steps.
* **`animation-iteration-count`** → how many times.

  * Number (e.g., `3`) or `infinite`.
* **`animation-direction`** → direction of playback.

  * `normal`, `reverse`, `alternate`, `alternate-reverse`.
* **`animation-delay`** → wait before start. Can be negative (starts midway).
* **`animation-play-state`** → `running` or `paused`.

  * Useful for hover/interaction.
* **`animation-fill-mode`** → what styles persist before/after.

  * `none`, `forwards`, `backwards`, `both`.

<br>

**4. Shorthand**
All properties can be combined:

```css
.my-element {
  animation: pulse 2s ease-in-out 0.5s infinite alternate both running;
}
```

Order:
`name → duration → timing → delay → iteration-count → direction → fill-mode → play-state`

<br>

**5. <mark>Accessibility: Reduced Motion</mark>**

* Users may prefer less animation.
* Detect with media query:

```css
@media (prefers-reduced-motion) {
  .autoplay-animation {
    animation-play-state: paused;
  }
}
```

<br>

✅ In short: **CSS animations let you move, fade, and transform elements smoothly with keyframes + animation properties, while respecting user preferences.**
