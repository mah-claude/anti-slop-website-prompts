# PROMPT

**Category:** Landing Page · **Source:** https://meez.design/p/prompt-hero · **License:** free to use, commercial projects OK

Copy everything inside the fence and paste it into Lovable, Bolt, v0, Cursor or Claude Code — don't trim it; the detail is the point.

````
### Overview

Build a full-screen, scroll-driven fashion/archive landing page for a brand called "prmpt". The page has two main phases:

1. **Hero phase** (first 100vh of scroll): Full-viewport video background with overlaid UI (logo, nav, product info, custom cursor). A black panel slides up from below covering the video.
2. **Gallery phase** (continues scrolling): The black panel contains a scattered grid of product images that scale in/out as they enter/exit the viewport. At the end, a white overlay fades in with a "view" CTA button.

---

### Tech Stack

- **React 19** + **TypeScript**
- **Vite 6** with `@vitejs/plugin-react`
- **Tailwind CSS v4** via `@tailwindcss/vite` plugin
- **GSAP 3.15** + `@gsap/react` (ScrollTrigger)
- **Motion (Framer Motion) 12** (`motion/react`)
- **Font**: "Inter Tight" (Google Fonts, weight 500) -- loaded via `<link>` or import

---

### Asset URLs

**Videos (CloudFront):**
- LEFT video: `https://meez.design/web/media/ext/5f14782b86025ef3.mp4`
- RIGHT video: `https://meez.design/web/media/ext/e9b7f55d37be8f40.mp4`

**Gallery Images (10 total, in order):**
1. `https://meez.design/web/media/ext/e64c05f1c0a2fd2a.webp`
2. `https://meez.design/web/media/ext/c4e53b540a38c5ff.webp`
3. `https://meez.design/web/media/ext/58b0aa7ffeff988e.webp`
4. `https://meez.design/web/media/ext/35730fb48d1fb44f.webp`
5. `https://meez.design/web/media/ext/3d5361051fe78cff.webp`
6. `https://meez.design/web/media/ext/69d5bd76b44a4172.webp`
7. `https://meez.design/web/media/ext/42f370af238a13cc.webp`
8. `https://meez.design/web/media/ext/e0c3503865c0922f.webp`
9. `https://meez.design/web/media/ext/387403738430a43f.webp`
10. `https://meez.design/web/media/ext/518026d4eccfb4d3.webp`

---

### SECTION 1: Hero (Video Background + Overlaid UI)

#### Root Container
- `id="scroll-spacer"`, `position: relative`, `user-select: none`, `background: white`
- Height is dynamically calculated (initially `500vh`, then overridden by GSAP to `vh + maxScroll + 2*vh`)
- Custom cursor hidden on desktop (`cursor: none`), default on touch devices

#### 1A. Custom Cursor (Desktop Only)
- Hidden on mobile/tablet (< 1024px)
- A `fixed`, `pointer-events-none`, `z-index: 50` div that follows `mousemove`
- Positioned via direct DOM manipulation (`style.left/top = clientX/clientY`)
- `transform: translate(-50%, -50%)` to center on pointer
- `mix-blend-mode: exclusion`
- Contains a 48x48 SVG: a circle with stroke (r=22.75, strokeWidth=2.5) containing a custom Japanese/decorative glyph path, all filled white

#### 1B. Logo (Top Left)
- `position: fixed`, `pointer-events-none`, `z-index: 20`
- `mix-blend-mode: exclusion`
- Responsive width: 124px (mobile < 640), 266px (tablet 640-1024), 355px (desktop)
- Position: `top: 16px, left: 16px` (mobile), `top: 32px, left: 32px` (desktop)
- Motion animation: fade in + slide up (`opacity: 0->1, y: 12->0`), duration 0.6s, ease `[0.25, 0.1, 0.25, 1]`, delay 0s
- SVG viewBox `0 0 355 110`, contains the "prmpt" wordmark + circled "R" mark, all paths filled white

#### 1C. Caption (Below Logo, Left Side)
- `position: fixed`, `pointer-events-none`, `z-index: 20`
- `mix-blend-mode: exclusion`
- Position: `left: 32px` (desktop), `left: 16px` (mobile)
- Top: 244px (desktop), 180px (tablet), 118px (mobile)
- Width: 692px (desktop), `calc(50vw - 48px)` (tablet), `calc(100vw - 32px)` (mobile)
- Font: Inter Tight, weight 500, size 12px, line-height 140%, letter-spacing -0.04em, color #FFFFFF
- Motion animation: same as logo but delay 0.3s
- Text content: "When switching between videos near the center, do not reset currentTime to 0 abruptly. Add a small dead zone: if cursor is within +/-50px of center, keep both videos at currentTime = 0 and show whichever was last active."

#### 1D. Header Navigation (Top Right)
- `position: fixed`, `z-index: 20`, `pointer-events-none`
- `mix-blend-mode: exclusion`
- Position: `top: 32px, right: 32px` (desktop), `top: 16px, right: 16px` (mobile)
- Width: 330px (desktop), auto (mobile)
- Height: 30px
- Flex row, justify-content: space-between, align-items: center
- Motion animation: same easing, delay 0.15s
- Contains:
  - "ABOUT" text (hidden on mobile): Inter Tight, 500, 15px, uppercase, white
  - A flex row with gap 50px (desktop) / 20px (mobile):
    - Hamburger SVG icon: viewBox `0 0 40 40`, two horizontal lines (`M0 14H40` and `M0 26H40`), stroke white, strokeWidth 2.5. Size: 30x30 (desktop), 24x24 (mobile)
    - "[ CART ]" text: Inter Tight, 500, 15px (desktop) / 13px (mobile), white

#### 1E. Product Info (Bottom Right)
- `id="outro-info"`, `position: fixed`, `pointer-events-none`, `z-index: 20`
- `mix-blend-mode: exclusion`
- **Desktop**: right: 32px, bottom: 80px, width: 330px, flex-column, align center
- **Mobile**: left: 0, right: 0, bottom: 48px, flex-column, align center
- Motion animation: opacity 0->1, delay 0.45s
- `data-outro-offset`: 166 (desktop), 132 (mobile) -- used by scroll animation
- Contains:
  - Top block (flex-column, align flex-start, width 100% desktop / 252px mobile, margin-bottom 32px desktop / 12px mobile):
    - Circle icon: relative div (30x30 desktop, 20x20 mobile) containing:
      - SVG circle (cx=20, cy=20, r=18.75, stroke white, strokeWidth 2.5 desktop / 2 mobile)
      - `<span id="circle-symbol">` centered inside, shows "8" initially, changes to random symbol from `['8', '$', '^^', '%', '/']` on scroll (throttled 80ms)
      - Font: Inter Tight, 500, 15px (desktop) / 10px (mobile), letter-spacing -0.04em, uppercase, white
    - Collection label: Inter Tight, 500, 30px (desktop) / 20px (mobile), line-height 100%, text-align center, letter-spacing -0.04em, uppercase, white. Content: `ARCHIVE COLLECTION` + line break + `"PROMPT"`
  - Price: Inter Tight, 500, 80px (desktop) / 60px (mobile), line-height 100%, text-align center, letter-spacing -0.04em, white. Content: `$97,33`

#### 1F. "View" Button (Bottom Right, Initially Hidden)
- `id="outro-buy"`, `position: fixed`, `pointer-events-none`, `z-index: 20`
- `mix-blend-mode: exclusion`
- **Desktop**: right: 32px, bottom: 32px, width: 330px, height: 174px
- **Mobile**: left: 16px, right: 16px, bottom: 60px, height: 100px
- `transform-origin: right bottom`, `transform: scale(0)` (starts hidden, scales to 1 via scroll)
- Background: #fff, border-radius: 1335px (pill shape)
- Flex center
- Text "view": Inter Tight, 500, 110px (desktop) / 72px (mobile), letter-spacing -0.04em, color #fff, `mix-blend-mode: exclusion`

#### 1G. Video Container
- `id="main-canvas"`, `pointer-events-none`
- **Desktop**: `position: fixed, inset: 0, width: 100%, height: 100%, z-index: 0`
- **Mobile**: `position: fixed, left: 0, top: 220px, width: 100vw, height: calc(100vh - 220px), z-index: 0`
- Opacity transition: 0 -> 1 when both videos loaded (`opacity 0.3s ease`)
- `overflow: hidden`
- Contains two `<video>` elements (muted, playsInline, preload="auto"), absolutely positioned to fill container, `object-fit: cover`
- Left video starts `display: none`, right starts `display: block`


**Desktop (non-touch):**
- Videos are NOT auto-played. They are scrubbed based on cursor X position via `requestAnimationFrame`.
- Dead zone: `Math.max(30, width * 0.05)` pixels from center
- If cursor is in dead zone, keep current video at `currentTime = 0`
- If cursor moves left of dead zone: show RIGHT video, scrub it based on distance from center-left-edge to left edge
- If cursor moves right of dead zone: show LEFT video, scrub it based on distance from center+deadzone to right edge
- `activeSideRef` tracks which side was last active, only changes when cursor exceeds dead zone
- Progress calculation: `(distance from dead zone edge) / (available range)` mapped to `0...video.duration`
CRITICAL: Only update currentTime when !video.seeking -- this prevents jittery playback by waiting for the browser to finish rendering the previous seek before requesting a new one.
#### 1H. Video Interaction Logic

**Mobile/Tablet (touch):**
- Videos auto-play alternately: left plays first, on `ended` event switches to right, on right `ended` switches back to left
- Respects `prefers-reduced-motion`

#### 1I. White Overlay
- `id="outro-overlay"`, `position: fixed, inset: 0`, `pointer-events-none`, `z-index: 12`
- Background: #fff, opacity: 0 (controlled by scroll)

#### 1J. Footer
- `id="outro-footer"`, `position: fixed`, `pointer-events-none`
- Left: 16px, bottom: 32px (desktop) / 24px (mobile)
- `mix-blend-mode: exclusion`, opacity: 0 (controlled by scroll)
- Flex row, gap: 80px (desktop) / space-between (mobile)
- Two spans: "PRMPT (R) 2026" and "PRIVACY POLICY"
- Font: Inter Tight, 500, 13px (desktop) / 11px (mobile), letter-spacing -0.02em, uppercase, white

---

### SECTION 2: Black Panel (Gallery)

#### Container
- `position: fixed, inset: 0`, background: black, `z-index: 10`
- Initially translated `translateY(100vh)` (off-screen below)
- Slides up to `translateY(0)` during first 100vh of scroll via GSAP ScrollTrigger (scrub: true, ease: none)

#### Inner Wrapper
- `width: 100%`, `padding-top: min(400px, 40vh)`

#### Grid Layout Algorithm
- Responsive columns: 2 (< 640px), 3 (640-1024px), 4 (>= 1024px)
- Each cell has `aspect-ratio: 2/3`
- Layout function `buildLayout(count, cols)` creates rows:
  - For each row `r`, compute primary column: `a = (r * 2 + (r % 2)) % cols`
  - Place one image at column `a`
  - Every 3rd row (`r % 3 === 0`), place a second image at `b = (a + 2) % cols` (or `(a+1)%cols` if same as a)
  - Empty cells get `-1` (rendered as empty spacer divs)

#### Card Behavior
- Each card has class `bp-card`, `will-change: transform`
- `transform: scale(0)` initially
- `transform-origin`: cards in left half of grid get `right bottom`, right half get `left bottom`
- Scale is computed per-frame in RAF based on card's vertical position:
  - **Enter**: `Math.min(1, (vh - top) / (vh * 0.6))` -- scales from 0 to 1 as it enters viewport
  - **Exit**: `Math.min(1, bottom / (vh * 0.4))` -- scales from 1 to 0 as it exits top
  - Final scale: `Math.min(enter, exit)`
  - If card is fully off-screen (bottom <= 0 or top >= vh): `scale(0)`

#### Scroll Phases (RAF-based, NOT scroll events)
- **Phase 1** (scrollY 0 to vh): Panel slides up. Cards are computed with panelOffset = `vh - scrollY`
- **Phase 2** (scrollY > vh): Panel is fixed at top. Inner wrapper translates up: `translateY(-(scrollY - vh))`. Cards recomputed with phase2 offset.
- **Outro** (scrollY > vh + maxScroll): White overlay fades in, product info slides up by `outroOffset` px, "view" button scales from 0 to 1, footer fades in. Progress: `(scrollY - vh - maxScroll) / (vh - 100)`

#### Spacer Height Calculation
- Set dynamically: `vh + maxScroll + 2 * vh` where `maxScroll = wrapScrollHeight - vh`

---

### CSS (index.css)

```css
@import "tailwindcss";

.bp-card {
  will-change: transform;
}

@media (prefers-reduced-motion: reduce) {
  .bp-card {
    will-change: auto;
  }
}
```

---

### Responsive Breakpoints
- **Mobile**: < 640px
- **Tablet**: 640px - 1024px
- **Desktop**: >= 1024px

---

### Key Design Principles
- All text overlays use `mix-blend-mode: exclusion` to remain visible against both light and dark backgrounds
- No visible scroll bar interaction -- entirely RAF-driven position tracking
- `pointer-events-none` on all overlaid UI elements
- `user-select: none` on root container
- Videos hidden (`visibility: hidden`) once scroll passes first viewport height
- Circle symbol randomizes on scroll (throttled to 80ms)
- Entry animations staggered: logo (0s), nav (0.15s), caption (0.3s), product info (0.45s)

### Source Code
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>prmpt</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@500&display=swap" rel="stylesheet"/>
<style>
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html, body { overflow-x: hidden; font-family: 'Inter Tight', sans-serif; font-weight: 500; }
body { background: #fff; }

#scroll-spacer {
  position: relative;
  user-select: none;
  -webkit-user-select: none;
  background: #fff;
  height: 500vh;
}

/* Custom Cursor */
#custom-cursor {
  position: fixed;
  pointer-events: none;
  z-index: 50;
  width: 48px;
  height: 48px;
  transform: translate(-50%, -50%);
  mix-blend-mode: exclusion;
  left: -100px;
  top: -100px;
}

/* Logo */
#logo {
  position: fixed;
  top: 32px;
  left: 32px;
  width: 355px;
  pointer-events: none;
  z-index: 20;
  mix-blend-mode: exclusion;
  opacity: 0;
  transform: translateY(12px);
  animation: fadeSlideIn 0.6s cubic-bezier(0.25, 0.1, 0.25, 1) 0s forwards;
}

/* Caption */
#caption {
  position: fixed;
  pointer-events: none;
  z-index: 20;
  left: 32px;
  top: 244px;
  width: 692px;
  font-size: 12px;
  line-height: 140%;
  letter-spacing: -0.04em;
  color: #fff;
  mix-blend-mode: exclusion;
  opacity: 0;
  transform: translateY(12px);
  animation: fadeSlideIn 0.6s cubic-bezier(0.25, 0.1, 0.25, 1) 0.3s forwards;
}

/* Header Nav */
#header-nav {
  position: fixed;
  z-index: 20;
  pointer-events: none;
  top: 32px;
  right: 32px;
  width: 330px;
  height: 30px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  mix-blend-mode: exclusion;
  opacity: 0;
  transform: translateY(12px);
  animation: fadeSlideIn 0.6s cubic-bezier(0.25, 0.1, 0.25, 1) 0.15s forwards;
}
#header-nav .nav-text {
  font-size: 15px;
  line-height: 18px;
  text-transform: uppercase;
  color: #fff;
}
#header-nav .nav-right {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 50px;
}

/* Product Info */
#outro-info {
  position: fixed;
  right: 32px;
  bottom: 80px;
  width: 330px;
  z-index: 20;
  display: flex;
  flex-direction: column;
  align-items: center;
  mix-blend-mode: exclusion;
  pointer-events: none;
  opacity: 0;
  animation: fadeIn 0.6s cubic-bezier(0.25, 0.1, 0.25, 1) 0.45s forwards;
}
#outro-info .info-top {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 100%;
  margin-bottom: 32px;
}
#outro-info .circle-icon {
  position: relative;
  width: 30px;
  height: 30px;
}
#outro-info .circle-icon svg {
  position: absolute;
  inset: 0;
}
#outro-info .circle-icon span {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 15px;
  line-height: 100%;
  letter-spacing: -0.04em;
  text-transform: uppercase;
  color: #fff;
}
#outro-info .collection-label {
  width: 100%;
  font-size: 30px;
  line-height: 100%;
  text-align: center;
  letter-spacing: -0.04em;
  text-transform: uppercase;
  color: #fff;
}
#outro-info .price {
  width: 100%;
  font-size: 80px;
  line-height: 100%;
  text-align: center;
  letter-spacing: -0.04em;
  color: #fff;
}

/* Buy Button */
#outro-buy {
  position: fixed;
  right: 32px;
  bottom: 32px;
  z-index: 20;
  width: 330px;
  height: 174px;
  transform-origin: right bottom;
  transform: scale(0);
  background: #fff;
  border-radius: 1335px;
  display: flex;
  justify-content: center;
  align-items: center;
  mix-blend-mode: exclusion;
  pointer-events: none;
}
#outro-buy span {
  font-size: 110px;
  line-height: 100%;
  text-align: center;
  letter-spacing: -0.04em;
  color: #fff;
  mix-blend-mode: exclusion;
}

/* Video Container */
#main-canvas {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  opacity: 0;
  transition: opacity 0.3s ease;
  overflow: hidden;
  pointer-events: none;
}
#main-canvas video {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* White Overlay */
#outro-overlay {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 12;
  background: #fff;
  opacity: 0;
}

/* Footer */
#outro-footer {
  position: fixed;
  left: 16px;
  bottom: 32px;
  z-index: 15;
  display: flex;
  align-items: center;
  gap: 80px;
  mix-blend-mode: exclusion;
  pointer-events: none;
  opacity: 0;
}
#outro-footer span {
  color: #fff;
  font-size: 13px;
  letter-spacing: -0.02em;
  text-transform: uppercase;
}

/* Black Panel */
#black-panel {
  position: fixed;
  inset: 0;
  background: #000;
  z-index: 10;
}
#black-panel .wrap {
  width: 100%;
  padding-top: min(400px, 40vh);
}
#black-panel .grid-row {
  display: flex;
  width: 100%;
}
#black-panel .grid-cell {
  flex: 1;
  aspect-ratio: 2/3;
}
#black-panel .bp-card {
  position: relative;
  height: 100%;
  width: 100%;
  transform: scale(0);
  will-change: transform;
}
#black-panel .bp-card img {
  height: 100%;
  width: 100%;
  object-fit: cover;
  -webkit-user-drag: none;
  user-drag: none;
}

@keyframes fadeSlideIn {
  to { opacity: 1; transform: translateY(0); }
}
@keyframes fadeIn {
  to { opacity: 1; }
}

/* Mobile */
@media (max-width: 639px) {
  #scroll-spacer { cursor: auto; }
  #custom-cursor { display: none; }
  #logo { top: 16px; left: 16px; width: 124px; }
  #caption { left: 16px; top: 118px; width: calc(100vw - 32px); }
  #header-nav { top: 16px; right: 16px; width: auto; }
  #header-nav .about-link { display: none; }
  #header-nav .nav-right { gap: 20px; }
  #header-nav .nav-text { font-size: 13px; }
  #outro-info { left: 0; right: 0; bottom: 48px; width: auto; }
  #outro-info .info-top { width: 252px; margin-bottom: 12px; align-self: center; }
  #outro-info .circle-icon { width: 20px; height: 20px; }
  #outro-info .circle-icon span { font-size: 10px; }
  #outro-info .collection-label { font-size: 20px; }
  #outro-info .price { font-size: 60px; }
  #outro-buy { left: 16px; right: 16px; bottom: 60px; width: auto; height: 100px; }
  #outro-buy span { font-size: 72px; }
  #main-canvas { top: 220px; height: calc(100vh - 220px); inset: unset; left: 0; width: 100vw; }
  #outro-footer { right: 16px; bottom: 24px; gap: 0; justify-content: space-between; }
  #outro-footer span { font-size: 11px; }
}

/* Tablet */
@media (min-width: 640px) and (max-width: 1023px) {
  #scroll-spacer { cursor: auto; }
  #custom-cursor { display: none; }
  #logo { width: 266px; }
  #caption { top: 180px; width: calc(50vw - 48px); }
}

@media (min-width: 640px) {
  #scroll-spacer { cursor: none; }
}

@media (prefers-reduced-motion: reduce) {
  .bp-card { will-change: auto; }
}
</style>
</head>
<body>
<div id="scroll-spacer">

  <!-- Custom Cursor (desktop) -->
  <div id="custom-cursor">
    <svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12.3 18.98C12.8733 19.0333 13.44 19.08 14 19.12C14.5733 19.1467 15.16 19.16 15.76 19.16C16.96 19.16 18.16 19.1067 19.36 19C20.56 18.8933 21.6733 18.74 22.7 18.54V20.48C21.6333 20.6533 20.5 20.78 19.3 20.86C18.1133 20.94 16.9267 20.9867 15.74 21C15.1533 21 14.58 20.9867 14.02 20.96C13.4733 20.9333 12.9067 20.9 12.32 20.86L12.3 18.98ZM19.56 15.48C19.5333 15.68 19.5067 15.8867 19.48 16.1C19.4667 16.3133 19.4533 16.52 19.44 16.72C19.4267 16.9467 19.4133 17.2467 19.4 17.62C19.4 17.9933 19.3933 18.4 19.38 18.84C19.38 19.2667 19.38 19.6933 19.38 20.12C19.38 20.96 19.3933 21.7667 19.42 22.54C19.46 23.3133 19.5 24.0467 19.54 24.74C19.58 25.4333 19.6133 26.0867 19.64 26.7C19.6667 27.3 19.68 27.8467 19.68 28.34C19.68 28.7933 19.62 29.2267 19.5 29.64C19.38 30.0533 19.18 30.42 18.9 30.74C18.62 31.06 18.24 31.3067 17.76 31.48C17.2933 31.6667 16.7133 31.76 16.02 31.76C14.66 31.76 13.6067 31.4933 12.86 30.96C12.1133 30.4267 11.74 29.68 11.74 28.72C11.74 28.1067 11.9067 27.56 12.24 27.08C12.5867 26.6 13.0733 26.22 13.7 25.94C14.34 25.66 15.1067 25.52 16 25.52C16.8933 25.52 17.7067 25.62 18.44 25.82C19.1733 26.0067 19.8533 26.2667 20.48 26.6C21.1067 26.92 21.6667 27.2733 22.16 27.66C22.6667 28.0467 23.1267 28.42 23.54 28.78L22.46 30.46C21.74 29.7667 21.02 29.1667 20.3 28.66C19.5933 28.1533 18.8733 27.76 18.14 27.48C17.4067 27.2 16.64 27.06 15.84 27.06C15.16 27.06 14.6067 27.1933 14.18 27.46C13.7667 27.7267 13.56 28.0733 13.56 28.5C13.56 28.9667 13.7667 29.32 14.18 29.56C14.5933 29.7867 15.12 29.9 15.76 29.9C16.2533 29.9 16.64 29.82 16.92 29.66C17.2 29.5 17.4 29.2667 17.52 28.96C17.64 28.6533 17.7 28.2933 17.7 27.88C17.7 27.5333 17.6867 27.0667 17.66 26.48C17.6333 25.88 17.6 25.2267 17.56 24.52C17.52 23.8 17.4867 23.0667 17.46 22.32C17.4333 21.56 17.42 20.8333 17.42 20.14C17.42 19.42 17.42 18.76 17.42 18.16C17.42 17.5467 17.42 17.08 17.42 16.76C17.42 16.5867 17.4067 16.38 17.38 16.14C17.3667 15.8867 17.34 15.6667 17.3 15.48H19.56ZM9.74 15.66C9.7 15.7667 9.65333 15.92 9.6 16.12C9.54667 16.32 9.49333 16.52 9.44 16.72C9.4 16.92 9.36667 17.08 9.34 17.2C9.27333 17.52 9.19333 17.9333 9.1 18.44C9.02 18.9333 8.93333 19.48 8.84 20.08C8.76 20.6667 8.68 21.2667 8.6 21.88C8.53333 22.4933 8.47333 23.08 8.42 23.64C8.38 24.2 8.36 24.6933 8.36 25.12C8.36 25.4667 8.37333 25.82 8.4 26.18C8.42667 26.5267 8.46667 26.8867 8.52 27.26C8.61333 26.98 8.72 26.6933 8.84 26.4C8.96 26.0933 9.08 25.7933 9.2 25.5C9.33333 25.2067 9.45333 24.94 9.56 24.7L10.56 25.48C10.3867 25.9867 10.2 26.5333 10 27.12C9.8 27.6933 9.62 28.24 9.46 28.76C9.31333 29.28 9.2 29.7133 9.12 30.06C9.09333 30.1933 9.06667 30.3533 9.04 30.54C9.02667 30.7133 9.02 30.86 9.02 30.98C9.03333 31.0733 9.04 31.1867 9.04 31.32C9.05333 31.4667 9.06667 31.6 9.08 31.72L7.3 31.86C7.08667 31.1533 6.9 30.26 6.74 29.18C6.59333 28.0867 6.52 26.86 6.52 25.5C6.52 24.7533 6.55333 23.98 6.62 23.18C6.68667 22.3667 6.76667 21.5733 6.86 20.8C6.96667 20.0267 7.06667 19.32 7.16 18.68C7.25333 18.04 7.33333 17.52 7.4 17.12C7.42667 16.8667 7.45333 16.5933 7.48 16.3C7.52 16.0067 7.54667 15.7267 7.56 15.46L9.74 15.66ZM32.32 15.22C32.2267 15.5133 32.1467 15.82 32.08 16.14C32.0267 16.46 31.9667 16.7667 31.9 17.06C31.8467 17.38 31.7733 17.7667 31.68 18.22C31.5867 18.66 31.48 19.14 31.36 19.66C31.2533 20.1667 31.14 20.68 31.02 21.2C30.9 21.72 30.7733 22.22 30.64 22.7C30.5067 23.1667 30.3733 23.5867 30.24 23.96C31.0933 23.4267 31.9533 23.0467 32.82 22.82C33.6867 22.58 34.6067 22.46 35.58 22.46C36.66 22.46 37.58 22.6333 38.34 22.98C39.1133 23.3133 39.7133 23.7867 40.14 24.4C40.5667 25.0133 40.78 25.7333 40.78 26.56C40.78 27.6267 40.52 28.5533 40 29.28C39.4933 30.0267 38.7733 30.6067 37.84 31.02C36.9067 31.4467 35.7933 31.72 34.5 31.84C33.22 31.96 31.7933 31.94 30.22 31.78L29.68 29.76C30.8133 29.92 31.9133 29.9933 32.98 29.98C34.06 29.9667 35.0267 29.8467 35.88 29.62C36.7333 29.38 37.4133 29.0133 37.92 28.52C38.4267 28.0267 38.68 27.3867 38.68 26.6C38.68 25.92 38.3933 25.3467 37.82 24.88C37.26 24.4 36.44 24.16 35.36 24.16C34.1867 24.16 33.0933 24.36 32.08 24.76C31.0667 25.16 30.24 25.7533 29.6 26.54C29.4933 26.6867 29.3933 26.8333 29.3 26.98C29.2067 27.1133 29.1133 27.2667 29.02 27.44L27.14 26.78C27.5267 26.0333 27.88 25.2 28.2 24.28C28.52 23.36 28.8 22.4333 29.04 21.5C29.2933 20.5533 29.5 19.68 29.66 18.88C29.82 18.08 29.9267 17.4267 29.98 16.92C30.0333 16.56 30.0667 16.2467 30.08 15.98C30.1067 15.7 30.1067 15.4133 30.08 15.12L32.32 15.22ZM25.78 17.68C26.3533 17.7733 27 17.8533 27.72 17.92C28.44 17.9867 29.1067 18.02 29.72 18.02C30.36 18.02 31.0667 18 31.84 17.96C32.6267 17.92 33.4467 17.86 34.3 17.78C35.1533 17.7 36.0067 17.6 36.86 17.48C37.7267 17.3467 38.56 17.1933 39.36 17.02L39.4 18.94C38.72 19.0467 37.9667 19.1533 37.14 19.26C36.3133 19.3667 35.4667 19.4667 34.6 19.56C33.7333 19.64 32.88 19.7067 32.04 19.76C31.2 19.8 30.4333 19.82 29.74 19.82C29.02 19.82 28.3267 19.8067 27.66 19.78C26.9933 19.74 26.3667 19.6933 25.78 19.64V17.68Z" fill="white"/>
      <circle cx="24" cy="24" r="22.75" stroke="white" stroke-width="2.5"/>
    </svg>
  </div>

  <!-- Logo -->
  <div id="logo">
    <svg width="100%" height="auto" viewBox="0 0 355 110" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M0 110L14.8228 22.3651H27.0028L25.2792 32.749H26.2559C27.2517 31.4177 28.554 29.8772 30.1626 28.1276C31.8096 26.3779 33.9737 24.8565 36.6548 23.5633C39.3359 22.232 42.6682 21.5664 46.6516 21.5664C51.8223 21.5664 56.2079 22.8596 59.8082 25.4461C63.4086 28.0325 65.9557 31.779 67.4494 36.6857C68.9815 41.5923 69.173 47.5069 68.024 54.4295C66.8749 61.2759 64.73 67.1715 61.5893 72.1162C58.4868 77.0228 54.6949 80.7884 50.2136 83.4129C45.7323 86.0373 40.8871 87.3686 35.6781 87.4066C31.8096 87.3686 28.7455 86.703 26.4857 85.4098C24.2642 84.1165 22.598 82.5951 21.4873 80.8454C20.3765 79.0958 19.5339 77.5553 18.9594 76.2241H18.2699L12.5821 110H0ZM34.7589 76.8517C38.4741 76.8136 41.7298 75.8247 44.5258 73.8849C47.3601 71.907 49.6966 69.2254 51.535 65.8402C53.4118 62.417 54.7141 58.5754 55.4418 54.3154C56.093 50.0934 56.0546 46.3088 55.3269 42.9616C54.6375 39.6145 53.2203 36.971 51.0754 35.0311C48.9305 33.0913 45.9621 32.1214 42.1703 32.1214C38.5316 32.1214 35.2951 33.0533 32.4608 34.917C29.6647 36.7427 27.3475 39.3292 25.509 42.6763C23.7088 45.9855 22.4448 49.8651 21.7171 54.3154C20.9894 58.7656 20.9894 62.6833 21.7171 66.0685C22.4448 69.4537 23.9003 72.0972 26.0835 73.999C28.2667 75.8627 31.1585 76.8136 34.7589 76.8517Z" fill="white"/>
      <path d="M63.522 86.1515L74.2082 22.3651H86.2732L84.5496 32.5778H85.2391C86.9626 29.1546 89.4906 26.454 92.8228 24.4761C96.1551 22.4602 99.698 21.4523 103.452 21.4523C104.256 21.4523 105.156 21.4713 106.152 21.5093C107.186 21.5474 108.048 21.6234 108.737 21.7376L106.669 33.6048C106.209 33.4526 105.348 33.3005 104.084 33.1483C102.82 32.9582 101.536 32.8821 100.234 32.9201C97.285 32.8821 94.5464 33.4907 92.0185 34.7459C89.5289 35.963 87.4223 37.6556 85.6987 39.8237C84.0134 41.9917 82.941 44.4831 82.4813 47.2977L76.0466 86.1515H63.522Z" fill="white"/>
      <path d="M99.2621 86.1515L109.948 22.3651H121.898L120.175 32.8631H121.037C122.952 29.3257 125.595 26.5681 128.965 24.5902C132.336 22.5743 136.147 21.5664 140.398 21.5664C144.611 21.5664 148.02 22.5743 150.625 24.5902C153.229 26.5681 154.915 29.3257 155.681 32.8631H156.37C158.477 29.4018 161.368 26.6632 165.045 24.6473C168.761 22.5934 172.916 21.5664 177.513 21.5664C183.296 21.5664 187.739 23.3921 190.842 27.0436C193.944 30.695 194.902 36.1532 193.714 43.418L186.475 86.1515H173.951L181.017 44.5591C181.707 40.223 181.017 37.1041 178.949 35.2023C176.919 33.3005 174.257 32.3306 170.963 32.2925C166.903 32.3306 163.532 33.5667 160.851 36.001C158.209 38.4353 156.562 41.5923 155.91 45.472L149.074 86.1515H136.664L143.788 43.7604C144.324 40.2991 143.692 37.5415 141.892 35.4876C140.092 33.3956 137.449 32.3306 133.964 32.2925C131.589 32.2925 129.291 32.9201 127.069 34.1753C124.848 35.4305 122.952 37.1421 121.381 39.3102C119.811 41.4782 118.796 43.9886 118.336 46.8413L111.787 86.1515H99.2621Z" fill="white"/>
      <path d="M183.872 110L198.694 22.3651H210.874L209.151 32.749H210.127C211.123 31.4177 212.425 29.8772 214.034 28.1276C215.681 26.3779 217.845 24.8565 220.526 23.5633C223.207 22.232 226.54 21.5664 230.523 21.5664C235.694 21.5664 240.079 22.8596 243.68 25.4461C247.28 28.0325 249.827 31.779 251.321 36.6857C252.853 41.5923 253.045 47.5069 251.895 54.4295C250.746 61.2759 248.602 67.1715 245.461 72.1162C242.358 77.0228 238.566 80.7884 234.085 83.4129C229.604 86.0373 224.759 87.3686 219.55 87.4066C215.681 87.3686 212.617 86.703 210.357 85.4098C208.136 84.1165 206.47 82.5951 205.359 80.8454C204.248 79.0958 203.405 77.5553 202.831 76.2241H202.141L196.454 110H183.872ZM218.63 76.8517C222.346 76.8136 225.601 75.8247 228.397 73.8849C231.232 71.907 233.568 69.2254 235.407 65.8402C237.283 62.417 238.586 58.5754 239.313 54.3154C239.964 50.0934 239.926 46.3088 239.198 42.9616C238.509 39.6145 237.092 36.971 234.947 35.0311C232.802 33.0913 229.834 32.1214 226.042 32.1214C222.403 32.1214 219.167 33.0533 216.332 34.917C213.536 36.7427 211.219 39.3292 209.38 42.6763C207.58 45.9855 206.316 49.8651 205.589 54.3154C204.861 58.7656 204.861 62.6833 205.589 66.0685C206.316 69.4537 207.772 72.0972 209.955 73.999C212.138 75.8627 215.03 76.8136 218.63 76.8517Z" fill="white"/>
      <path d="M284.54 22.3651L282.874 32.3496H247.828L249.494 22.3651H284.54ZM261.387 7.1888H273.911L263.742 67.4378C263.359 69.796 263.417 71.6027 263.915 72.8579C264.451 74.075 265.274 74.8928 266.385 75.3112C267.496 75.6916 268.741 75.8817 270.119 75.8817C271.154 75.9198 272.035 75.8817 272.762 75.7676C273.528 75.6155 274.122 75.5014 274.543 75.4253L275.233 85.695C274.39 85.9613 273.26 86.2465 271.843 86.5508C270.426 86.8551 268.721 86.9882 266.73 86.9502C263.436 87.0263 260.467 86.4557 257.825 85.2386C255.182 84.0214 253.209 82.1387 251.907 79.5902C250.605 77.0038 250.279 73.7898 250.93 69.9481L261.387 7.1888Z" fill="white"/>
      <path d="M309.727 48.1535V17.5726H325.182C326.676 17.5346 328.189 17.8959 329.721 18.6566C331.253 19.3793 332.536 20.4824 333.57 21.9658C334.604 23.4111 335.121 25.2178 335.121 27.3859C335.121 29.592 334.585 31.4938 333.513 33.0913C332.44 34.6508 331.119 35.8299 329.548 36.6286C327.978 37.3893 326.389 37.7697 324.78 37.7697H313.806V32.5207H322.827C323.822 32.5588 324.818 32.1594 325.814 31.3226C326.81 30.4478 327.308 29.1355 327.308 27.3859C327.308 25.6362 326.791 24.4381 325.757 23.7915C324.761 23.1068 323.822 22.7645 322.941 22.7645H316.966V48.1535H309.727ZM328.802 33.7759L336.27 48.1535H328.342L321.103 33.7759H328.802ZM321.563 66.4108C316.966 66.4108 312.638 65.555 308.578 63.8434C304.557 62.0937 301.014 59.6974 297.95 56.6546C294.885 53.6117 292.492 50.0934 290.768 46.0996C289.044 42.0678 288.183 37.7697 288.183 33.2054C288.183 28.6411 289.044 24.362 290.768 20.3683C292.492 16.3364 294.885 12.7991 297.95 9.75622C301.014 6.71335 304.557 4.3361 308.578 2.62448C312.638 0.874827 316.966 0 321.563 0C326.197 0 330.525 0.874827 334.547 2.62448C338.607 4.3361 342.169 6.71335 345.233 9.75622C348.297 12.7991 350.691 16.3364 352.415 20.3683C354.138 24.362 355 28.6411 355 33.2054C355 37.7697 354.138 42.0678 352.415 46.0996C350.691 50.0934 348.297 53.6117 345.233 56.6546C342.207 59.6974 338.664 62.0937 334.604 63.8434C330.544 65.555 326.197 66.4108 321.563 66.4108ZM321.563 58.138C326.235 58.138 330.468 57.0349 334.26 54.8288C338.09 52.5847 341.135 49.5799 343.395 45.8143C345.654 42.0107 346.765 37.8077 346.727 33.2054C346.765 28.603 345.654 24.4191 343.395 20.6535C341.135 16.8499 338.09 13.8451 334.26 11.639C330.468 9.39488 326.235 8.27282 321.563 8.27282C316.966 8.27282 312.753 9.39488 308.923 11.639C305.131 13.8451 302.105 16.8499 299.845 20.6535C297.586 24.4191 296.456 28.603 296.456 33.2054C296.456 37.8077 297.586 42.0107 299.845 45.8143C302.105 49.5799 305.131 52.5847 308.923 54.8288C312.753 57.0349 316.966 58.138 321.563 58.138Z" fill="white"/>
    </svg>
  </div>

  <!-- Caption -->
  <p id="caption">When switching between videos near the center, do not reset currentTime to 0 abruptly. Add a small dead zone: if cursor is within &plusmn;50px of center, keep both videos at currentTime = 0 and show whichever was last active.</p>

  <!-- Header Nav -->
  <div id="header-nav">
    <span class="nav-text about-link">ABOUT</span>
    <div class="nav-right">
      <svg width="30" height="30" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 14H40M0 26H40" stroke="white" stroke-width="2.5"/>
      </svg>
      <span class="nav-text">[ CART ]</span>
    </div>
  </div>

  <!-- Product Info -->
  <div id="outro-info" data-outro-offset="166">
    <div class="info-top">
      <div class="circle-icon">
        <svg width="30" height="30" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="20" cy="20" r="18.75" stroke="white" stroke-width="2.5"/>
        </svg>
        <span id="circle-symbol">8</span>
      </div>
      <span class="collection-label">ARCHIVE COLLECTION<br>&quot;PROMPT&quot;</span>
    </div>
    <span class="price">$97,33</span>
  </div>

  <!-- Buy Button -->
  <div id="outro-buy">
    <span>view</span>
  </div>

  <!-- Videos -->
  <div id="main-canvas">
    <video id="video-left" src="https://meez.design/web/media/ext/5f14782b86025ef3.mp4" muted playsinline preload="auto" style="display:none;"></video>
    <video id="video-right" src="https://meez.design/web/media/ext/e9b7f55d37be8f40.mp4" muted playsinline preload="auto" style="display:block;"></video>
  </div>

  <!-- White Overlay -->
  <div id="outro-overlay"></div>

  <!-- Footer -->
  <div id="outro-footer">
    <span>PRMPT&reg; 2026</span>
    <span>PRIVACY POLICY</span>
  </div>

  <!-- Black Panel -->
  <div id="black-panel">
    <div class="wrap" id="panel-wrap"></div>
  </div>

</div>

<script>
(function() {
  const CARDS = [
    "https://meez.design/web/media/ext/e64c05f1c0a2fd2a.webp",
    "https://meez.design/web/media/ext/c4e53b540a38c5ff.webp",
    "https://meez.design/web/media/ext/58b0aa7ffeff988e.webp",
    "https://meez.design/web/media/ext/35730fb48d1fb44f.webp",
    "https://meez.design/web/media/ext/3d5361051fe78cff.webp",
    "https://meez.design/web/media/ext/69d5bd76b44a4172.webp",
    "https://meez.design/web/media/ext/42f370af238a13cc.webp",
    "https://meez.design/web/media/ext/e0c3503865c0922f.webp",
    "https://meez.design/web/media/ext/387403738430a43f.webp",
    "https://meez.design/web/media/ext/518026d4eccfb4d3.webp",
  ];

  // Responsive helpers
  function isMobile() { return window.innerWidth < 640; }
  function isTablet() { return window.innerWidth >= 640 && window.innerWidth < 1024; }
  function isTouch() { return isMobile() || isTablet(); }
  function getCols() {
    if (window.innerWidth < 640) return 2;
    if (window.innerWidth < 1024) return 3;
    return 4;
  }

  // Build scattered grid layout
  function buildLayout(count, cols) {
    var rows = [];
    var i = 0, r = 0;
    while (i < count) {
      var row = new Array(cols).fill(-1);
      var a = (r * 2 + (r % 2)) % cols;
      row[a] = i++;
      if (r % 3 === 0 && i < count) {
        var b = (a + 2) % cols;
        if (b === a) b = (a + 1) % cols;
        row[b] = i++;
      }
      rows.push(row);
      r++;
    }
    return rows;
  }

  // Render grid
  function renderGrid() {
    var cols = getCols();
    var layout = buildLayout(CARDS.length, cols);
    var wrap = document.getElementById('panel-wrap');
    wrap.innerHTML = '';
    layout.forEach(function(row) {
      var rowDiv = document.createElement('div');
      rowDiv.className = 'grid-row';
      row.forEach(function(idx, ci) {
        var cell = document.createElement('div');
        cell.className = 'grid-cell';
        if (idx !== -1) {
          var card = document.createElement('div');
          card.className = 'bp-card';
          card.dataset.col = ci;
          var img = document.createElement('img');
          img.src = CARDS[idx];
          img.alt = '';
          img.draggable = false;
          card.appendChild(img);
          cell.appendChild(card);
        }
        rowDiv.appendChild(cell);
      });
      wrap.appendChild(rowDiv);
    });
  }

  renderGrid();
  window.addEventListener('resize', renderGrid);

  // Circle symbol randomizer
  var symbols = ['8', '$', '^^', '%', '/'];
  var lastSymbolTime = 0;
  window.addEventListener('scroll', function() {
    var now = Date.now();
    if (now - lastSymbolTime < 80) return;
    lastSymbolTime = now;
    var el = document.getElementById('circle-symbol');
    if (el) el.textContent = symbols[Math.floor(Math.random() * symbols.length)];
  }, { passive: true });

  // Video loading
  var vl = document.getElementById('video-left');
  var vr = document.getElementById('video-right');
  var canvas = document.getElementById('main-canvas');
  var readyCount = 0;
  function checkReady() {
    readyCount++;
    if (readyCount >= 2) canvas.style.opacity = '1';
  }
  vl.addEventListener('loadeddata', checkReady, { once: true });
  vr.addEventListener('loadeddata', checkReady, { once: true });
  if (vl.readyState >= 2) checkReady();
  if (vr.readyState >= 2) checkReady();

  // Video interaction
  var targetX = window.innerWidth / 2;
  var activeSide = 'right';
  var cursorEl = document.getElementById('custom-cursor');

  if (isTouch()) {
    // Mobile: auto-play alternating
    vl.style.display = 'block';
    vr.style.display = 'none';
    vl.currentTime = 0;
    vl.play();
    vl.addEventListener('ended', function() {
      vl.style.display = 'none';
      vr.style.display = 'block';
      vr.currentTime = 0;
      vr.play();
    });
    vr.addEventListener('ended', function() {
      vr.style.display = 'none';
      vl.style.display = 'block';
      vl.currentTime = 0;
      vl.play();
    });
  }

  // Desktop: cursor tracking + video scrub
  window.addEventListener('mousemove', function(e) {
    targetX = e.clientX;
    if (cursorEl) {
      cursorEl.style.left = e.clientX + 'px';
      cursorEl.style.top = e.clientY + 'px';
    }
  });
  window.addEventListener('touchmove', function(e) {
    if (e.touches.length > 0) targetX = e.touches[0].clientX;
  }, { passive: true });
  window.addEventListener('touchstart', function(e) {
    if (e.touches.length > 0) targetX = e.touches[0].clientX;
  }, { passive: true });

  // Scroll-driven animation (RAF)
  var panel = document.getElementById('black-panel');
  var wrap = document.getElementById('panel-wrap');
  var outroOverlay = document.getElementById('outro-overlay');
  var outroInfo = document.getElementById('outro-info');
  var outroBuy = document.getElementById('outro-buy');
  var outroFooter = document.getElementById('outro-footer');
  var spacer = document.getElementById('scroll-spacer');
  var mainCanvas = document.getElementById('main-canvas');

  var vh, maxScroll, naturalTops, naturalHeights, items, cols;
  var initialized = false;

  function measure() {
    vh = window.innerHeight;
    cols = getCols();

    // Position panel initially
    panel.style.transform = 'translateY(' + vh + 'px)';

    items = Array.from(panel.querySelectorAll('.bp-card'));
    naturalTops = items.map(function(el) {
      var top = 0;
      var node = el;
      while (node && node !== wrap) {
        top += node.offsetTop;
        node = node.offsetParent;
      }
      return top;
    });
    naturalHeights = items.map(function(el) { return el.offsetHeight; });

    maxScroll = Math.max(0, wrap.scrollHeight - vh);
    spacer.style.height = (vh + maxScroll + 2 * vh) + 'px';

    items.forEach(function(el) {
      var ci = Number(el.dataset.col || 0);
      el.style.transformOrigin = ci < cols / 2 ? 'right bottom' : 'left bottom';
    });

    initialized = true;
  }

  // Delay measure to let images start loading and layout settle
  setTimeout(measure, 100);
  window.addEventListener('resize', function() {
    setTimeout(measure, 50);
  });

  function scaleCards(panelOffset, phase2) {
    if (!items) return;
    items.forEach(function(el, i) {
      var top = naturalTops[i] - phase2 + panelOffset;
      var bottom = top + naturalHeights[i];
      if (bottom <= 0 || top >= vh) {
        el.style.transform = 'scale(0)';
        return;
      }
      var enter = Math.min(1, Math.max(0, (vh - top) / (vh * 0.6)));
      var exit = Math.min(1, Math.max(0, bottom / (vh * 0.4)));
      el.style.transform = 'scale(' + Math.min(enter, exit) + ')';
    });
  }

  var lastSy = -1;
  var inPhase2 = false;

  function tick() {
    if (!initialized) { requestAnimationFrame(tick); return; }

    var sy = window.scrollY;

    // Video scrub (desktop only)
    if (!isTouch() && vl.duration && vr.duration) {
      var width = window.innerWidth || 1000;
      var centerX = width / 2;
      var currentX = Math.max(0, Math.min(width, targetX));
      var deadZonePx = Math.max(30, width * 0.05);
      var dist = currentX - centerX;
      var absDist = Math.abs(dist);

      if (absDist > deadZonePx) {
        activeSide = dist < 0 ? 'left' : 'right';
      }

      if (activeSide === 'left') {
        vr.style.display = 'block';
        vl.style.display = 'none';
        if (!vr.seeking) {
          if (absDist <= deadZonePx) {
            vr.currentTime = 0;
          } else {
            var progress = (centerX - deadZonePx - currentX) / Math.max(1, centerX - deadZonePx);
            vr.currentTime = Math.max(0, Math.min(vr.duration, progress * vr.duration));
          }
        }
      } else {
        vl.style.display = 'block';
        vr.style.display = 'none';
        if (!vl.seeking) {
          if (absDist <= deadZonePx) {
            vl.currentTime = 0;
          } else {
            var progress = (currentX - (centerX + deadZonePx)) / Math.max(1, width - centerX - deadZonePx);
            vl.currentTime = Math.max(0, Math.min(vl.duration, progress * vl.duration));
          }
        }
      }
    }

    if (sy === lastSy) { requestAnimationFrame(tick); return; }
    lastSy = sy;

    // Hide video canvas after first vh
    if (mainCanvas) mainCanvas.style.visibility = sy >= vh ? 'hidden' : 'visible';

    // Phase 1: panel slides up
    if (sy < vh) {
      var panelY = vh - sy;
      panel.style.transform = 'translateY(' + panelY + 'px)';

      if (inPhase2) {
        inPhase2 = false;
        wrap.style.transform = 'translateY(0px)';
        if (outroOverlay) outroOverlay.style.opacity = '0';
        if (outroInfo) outroInfo.style.transform = 'translateY(0px)';
        if (outroBuy) outroBuy.style.transform = 'scale(0)';
        if (outroFooter) outroFooter.style.opacity = '0';
      }
      scaleCards(panelY, 0);
      requestAnimationFrame(tick);
      return;
    }

    // Phase 2: panel fixed, content scrolls
    panel.style.transform = 'translateY(0px)';
    inPhase2 = true;
    var phase2 = Math.min(sy - vh, maxScroll);
    wrap.style.transform = 'translateY(' + (-phase2) + 'px)';

    // Outro progress
    var outroProgress = Math.min(1, Math.max(0, (sy - vh - maxScroll) / (vh - 100)));
    if (outroOverlay) outroOverlay.style.opacity = String(outroProgress);
    if (outroInfo) {
      var outroOffset = Number(outroInfo.dataset.outroOffset || 166);
      outroInfo.style.transform = 'translateY(' + (-outroProgress * outroOffset) + 'px)';
    }
    if (outroBuy) outroBuy.style.transform = 'scale(' + outroProgress + ')';
    if (outroFooter) outroFooter.style.opacity = String(outroProgress);

    scaleCards(0, phase2);
    requestAnimationFrame(tick);
  }

  requestAnimationFrame(tick);
})();
</script>
</body>
</html>
````
