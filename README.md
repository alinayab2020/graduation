# MAZUMS Cinematic Luxe — Ultra Smooth Scroll Cinema

A premium, performance-first graduation landing page for Mazandaran University of Medical Sciences.

## Design direction

The scroll-scrubbed film remains the opening interaction. The later chapters now feel richer again, but the visual effects are built from lightweight composited layers rather than a continuously rendered 3D engine.

Added in the Cinematic Luxe edition:

- layered cyan/gold aurora light
- scroll-driven optical orbit/depth rings
- baked stardust and light particles
- cinematic light-fan rays
- perspective horizon/grid accents
- multi-band optical scene transitions
- premium frame/HUD details
- local glass-like copy panels without runtime backdrop blur
- subtle desktop pointer parallax on decorative layers only
- richer graduation confetti with container-level animation variables
- scene-specific cyan/gold art direction while preserving one continuous visual language
- automatic lighter FX tier on slow networks / Save-Data / lower-power mobile devices

## Performance guardrails

- No Three.js/WebGL.
- No Canvas video redraw.
- No bloom post-processing.
- No moving full-screen `filter: blur()` or `mix-blend-mode` layers.
- No GSAP, ScrollTrigger or Lenis dependency.
- Scroll work is coalesced to one `requestAnimationFrame`.
- Hero video renders directly in the browser video element.
- Latest scroll target wins; stale seeks are not queued.
- Desktop and mobile scrub videos are separate optimized H.264 assets.
- Chapter images are pre-warmed during idle time after the hero is ready.
- Added decorative layers are transform/opacity driven and stop doing work when the page is idle.
- Confetti uses two container variables instead of per-particle JS updates every frame.

## GitHub Pages

Upload the contents of this folder directly to the repository root, commit to `main`, then use:

**Settings → Pages → Deploy from a branch → main / root**

No build step is required. All asset paths are relative and work under a project URL such as `/mg/`.
