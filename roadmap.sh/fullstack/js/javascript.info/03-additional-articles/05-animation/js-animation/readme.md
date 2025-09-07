
# 🎨 CSS Animations

### 🔹 Basics
- CSS animations allow smooth transitions without JavaScript.  
- Controlled by **transition** and **@keyframes**.  
- JavaScript can enhance/trigger them if needed.

<br>

## 1. CSS Transitions
- Animate property changes over time.  
- Triggered automatically when property changes.  

**Main properties:**
1. `transition-property` → which CSS properties to animate.  
2. `transition-duration` → how long the animation lasts (`s` / `ms`).  
3. `transition-delay` → wait time before animation starts (can be negative).  
4. `transition-timing-function` → speed curve of animation.  

✅ Can combine multiple transitions in shorthand:  
```css
transition: font-size 3s, color 2s;
```

<br>

## 2. Transition Timing
### Bezier Curves (`cubic-bezier(x2,y2,x3,y3)`)
- `(0,0)` → start, `(1,1)` → end, x in `[0..1]`, y can be any value.  
- Defines acceleration/deceleration of animation.  

Common curves:
- `linear` → constant speed (`cubic-bezier(0,0,1,1)`).  
- `ease` (default) → smooth acceleration/deceleration.  
- `ease-in` → starts slow, ends fast.  
- `ease-out` → starts fast, ends slow.  
- `ease-in-out` → slow start and end, faster middle.  

### Steps (`steps(n, start/end)`)
- Break animation into discrete steps.  
- `start` → first change happens immediately.  
- `end` → first change happens at the end of the first interval.  
- Shorthands:  
  - `step-start` = `steps(1, start)`  
  - `step-end` = `steps(1, end)`  

<br>

## 3. Event: `transitionend`
- Fires when a CSS transition finishes.  
- Useful to **chain animations** or trigger JS after animation.  

Event object:
- `event.propertyName` → property that finished.  
- `event.elapsedTime` → duration (without delay).  

<br>

## 4. CSS Keyframes
- Use `@keyframes` to define multiple animation stages.  
- Attach with `animation` property:  

```css
@keyframes move {
  from { left: 0; }
  to { left: 100px; }
}
.box {
  animation: move 3s infinite alternate;
}
```

**Animation properties:**
- `animation-name`  
- `animation-duration`  
- `animation-iteration-count` (e.g., `infinite`)  
- `animation-direction` (`normal | reverse | alternate`)  
- `animation-delay`  
- `animation-timing-function`

<br>

## 5. Performance
- Animating some CSS properties is **expensive** (triggers Layout + Paint + Composite).  
- Best for performance:  
  - `transform` (translate, scale, rotate, skew).  
  - `opacity`.  
- These often use **GPU acceleration**.  
- Avoid animating: `left`, `top`, `width`, `height` (cause layout recalculations).  

<br>

## 6. CSS vs JavaScript Animations
✅ CSS Advantages:  
- Simple, lightweight.  
- Browser-optimized.  
- Great for most UI transitions.  

❌ CSS Limitations:  
- Restricted to property changes.  
- No custom logic (e.g., physics, explosions).  
- Can’t create/destroy elements during animation.  

JS Animations → more **flexible**, for complex effects.

<br>

## 7. Tasks (examples)
1. **Animate a plane** → grows from small to big (with transitionend → show "Done!").  
2. **Flying plane** → overshoots size, then returns.  
3. **Animated circle** → expand circle dynamically.  
4. **Animated circle with callback** → run function after animation completes.

<br>

⚡ **Summary**:  
- Use **CSS transitions** for simple property changes.  
- Use **keyframes** for multi-stage animations.  
- Prefer `transform` + `opacity` for performance.  
- JavaScript can control animations (trigger, chain, or wait for `transitionend`).  
