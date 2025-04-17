# 🌊 Fluid Simulation Background for React (Based on Pavel Dobryakov's Script)

This repo is a lightweight, mobile-friendly implementation of Pavel Dobryakov’s [WebGL Fluid Simulation](https://paveldogreat.github.io/WebGL-Fluid-Simulation/), adapted to work inside a modern React project.

It adds a **playful cursor animation** that reacts to mouse/touch movement — a great way to elevate your portfolio or add interactive vibes to any part of your site.

---

## 🚀 Quick Intro

This is a React-friendly refactor of Pavel’s original script, with guidance on:
- Integrating the simulation as a **background canvas**
- Ensuring **clickable elements (buttons, links, nav)** still work above the animation
- Making the layout **mobile responsive**
- Customizing interactivity with simple config tweaks

---

## 🔧 Step-by-Step Setup

### 1. Place the Files
Drop the following into your `/public` folder:
- `script.js` (fluid simulation logic)
- `dat.gui.min.js` (optional for GUI, or can be removed if unused)

### 2. Reference Container in Your Component
Wrap your homepage or desired section in a div with a `ref` called `containerRef`.

Example:
  const containerRef = useRef(null);
  
  return (
    <div id="intro" ref={containerRef}>
      {/* your content */}
    </div>
  );

3. Add Canvas for Simulation
Inside your JSX, add a <canvas> element with a ref={canvasRef}.
This is required for the simulation to attach to.


4.  Load the Script
Use a useEffect to dynamically load and initialize script.js. Here's a simplified version:

5. Adjust Your CSS
To make sure the canvas stays behind your content:


## ⚠️ Common Errors & Fixes

> 💡 **Tip:** You can adjust the behavior of the simulation by modifying the `config` object at the beginning of the script. This includes settings for resolution, interactivity, and whether the animation should run on mobile.

---

### 🧩 1. Buttons or Links Not Clickable

Even though the canvas animation appears correctly in the background, clickable elements (like buttons or links) may not respond.

**Cause:**  
The canvas is set with `pointer-events: none` to allow content to sit on top. But any interactive element overlapping it must explicitly allow interactions.

**✅ Fix:**  
Add the following CSS to clickable elements:
```css
pointer-events: auto;
```
### 📱 Error 2: Scrollability Issues on Mobile

**Problem:**  
The fluid animation works, but the page becomes unscrollable on mobile devices.

**Cause:**  
The default interaction listeners in `script.js` (e.g. `touchstart`, `touchmove`) can block native scrolling on touch devices. These are usually commented out by default to prevent scroll interference.

---

**✅ Fix Options:**

1. **Uncomment scroll-related event listeners in `script.js`**  
   If you need touch interactivity (e.g. dragging on canvas), but also want scrollability:
   - Uncomment the `touchstart`, `touchmove`, and related listeners.
   - Be aware this may cause the animation to misbehave or freeze on certain devices.

2. **Restrict animation to desktop only (Recommended for simplicity)**  
   On [madebydianna.com](https://madebydianna.com), the animation is disabled for mobile by default.

   **Suggested setup:**
   - Set canvas to `position: fixed`
   - Allow pointer interaction only when necessary
   - Add a scroll trigger/button to guide users to the next section

   ```css
   canvas {
     position: fixed;
     top: 0;
     left: 0;
     width: 100%;
     height: 100%;
     pointer-events: none; /* allows clicks to pass through */
   }

   .scroll-hint {
     position: absolute;
     bottom: 10%;
     width: 100%;
     text-align: center;
     pointer-events: auto;
   }
```
