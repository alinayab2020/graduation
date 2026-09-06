# Performance / visual-effects audit — Cinematic Luxe edition

## Performance problems intentionally kept out

The earlier heavy version combined scroll-video decoding with a full-screen Canvas copy, runtime blur, continuous Three.js/WebGL rendering, bloom post-processing, particle geometry updates and several large blend/filter layers. Those systems competed for the decoder, main thread and GPU during scroll.

The optimized architecture still avoids all of those bottlenecks.

## Effects restored safely

The Cinematic Luxe edition restores visual density with a different implementation:

1. **Stardust:** one 22 KB baked alpha texture, moved only with compositor transforms.
2. **Aurora:** static radial-gradient layers; only transform and parent opacity change during scrolling.
3. **Optical rings:** CSS borders/pseudo-elements in a single perspective group, with one group transform.
4. **Light fan:** three clipped gradient planes with transform-only movement.
5. **Horizon/grid:** static painted layers; no JS geometry and no render loop.
6. **Scene transition:** three gradient bands inside one transition layer; no runtime filter.
7. **Text luminance bed:** local translucent gradient panels instead of `backdrop-filter`.
8. **Pointer parallax:** desktop-only, decorative-only, throttled to one animation frame.
9. **Graduation confetti:** per-particle starting values are static. Scrolling updates only two variables on the container.
10. **Adaptive quality:** slow network, Save-Data, reduced-motion and lower-power mobile devices automatically remove secondary FX.

## Loading / scrub behavior

- Hero scrub master: H.264, 540×960, 231 frames, 15 fps.
- Mobile scrub master: H.264, 360×640, 231 frames, 15 fps.
- Both use short GOPs and are designed for accurate scroll seeking.
- The hero file is prebuffered before the loader exits when possible.
- Chapter images are loaded ahead; on normal connections the remaining chapter imagery is warmed during idle time after the hero becomes ready.
- A failed prebuffer automatically falls back to normal streamed playback.

## Static verification performed on this edition

- JavaScript syntax: passed.
- HTML parse: passed.
- CSS parse: passed.
- All local HTML/CSS asset references resolve: passed.
- GitHub Pages relative paths: passed.
- Desktop video metadata: H.264, 540×960, 15 fps, 231 frames.
- Mobile video metadata: H.264, 360×640, 15 fps, 231 frames.
- No Canvas element or Three.js/WebGL engine added.
- No runtime full-screen blur or mix-blend layer added.

The design keeps the measured performance-first architecture of the prior optimized build while restoring visual richness with compositor-friendly layers.
