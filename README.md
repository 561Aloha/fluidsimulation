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

<canvas ref={canvasRef} />

useEffect(() => {
  const fluidScript = document.createElement('script');
  fluidScript.src = '/script.js';
  fluidScript.async = true;

  fluidScript.onload = () => {
    if (window.initFluidSimulation && canvasRef.current && containerRef.current) {
      window.initFluidSimulation(canvasRef.current, containerRef.current);
    }
  };

  document.body.appendChild(fluidScript);

  return () => {
    if (document.body.contains(fluidScript)) {
      document.body.removeChild(fluidScript);
    }
  };
}, []);

4.  Load the Script
Use a useEffect to dynamically load and initialize script.js. Here's a simplified version:

jsx

useEffect(() => {
  const fluidScript = document.createElement('script');
  fluidScript.src = '/script.js';
  fluidScript.async = true;

  fluidScript.onload = () => {
    if (window.initFluidSimulation && canvasRef.current && containerRef.current) {
      window.initFluidSimulation(canvasRef.current, containerRef.current);
    }
  };

  document.body.appendChild(fluidScript);

  return () => {
    if (document.body.contains(fluidScript)) {
      document.body.removeChild(fluidScript);
    }
  };
}, []);

5. Adjust Your CSS
To make sure the canvas stays behind your content:

css

canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 0;
  pointer-events: none;
}
🎨 Customizing the Simulation
All the magic happens inside script.js. At the top, you'll find the config object:

js

let config = {
  SIM_RESOLUTION: 128,
  DYE_RESOLUTION: 1024,
  DENSITY_DISSIPATION: 2.0,
  VELOCITY_DISSIPATION: 1.33,
  PRESSURE: 0.24,
  PRESSURE_ITERATIONS: 3,
  CURL: 30,
  SPLAT_RADIUS: 0.03,
  SPLAT_FORCE: 6000,
  SHADING: true,
  COLORFUL: true,
  COLOR_UPDATE_SPEED: 10,
  ...
}
👉 You can play around with different values and see how they affect behavior here:
Pavel’s Live Fluid Playground

