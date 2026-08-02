# Cargo Group

**Category:** Hero · **Source:** https://meez.design/p/cargo-group · **License:** free to use, commercial projects OK

Copy everything inside the fence and paste it into Lovable, Bolt, v0, Cursor or Claude Code — don't trim it; the detail is the point.

````
Create a full-viewport hero section for "CARGOX GROUP" logistics company using React, Tailwind CSS, Framer Motion (`motion` package from npm - import from `motion/react`), and `lucide-react` for the hamburger icon.

## Tech Stack
- React 18 + TypeScript + Vite
- Tailwind CSS 3
- `motion` package (v12+) - import `{ motion, AnimatePresence }` from `motion/react`
- `lucide-react` for Menu/X icons
- Google Font: `Barlow Condensed` weight 800 (imported in CSS via `@import url('https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@800&display=swap')`)

## Global CSS
```css
@import url('https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@800&display=swap');
@tailwind base;
@tailwind components;
@tailwind utilities;

* { margin: 0; padding: 0; box-sizing: border-box; }
html, body, #root { height: 100%; overflow: hidden; }
body { font-family: Helvetica, Arial, sans-serif; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }
```

## Layout Structure
Single full-viewport (`min-height: 100vh`) flex column with `overflow: hidden` and dark fallback `backgroundColor: '#1a1a2e'`. All content is layered above a fullscreen video background.

## Video Background
- Absolute positioned, `inset-0`, `object-cover`, `z-0`
- Attributes: `autoPlay`, `muted`, `loop`, `playsInline`
- URL: `https://meez.design/web/media/ext/597d53d9b15f2d2d.mp4`
- On `onCanPlay`, set a `videoReady` state to `true`
- All content below is wrapped in `<AnimatePresence>` and only renders when `videoReady === true`, fading in with `opacity: 0 -> 1` over 0.3s. The wrapper div uses `className="flex flex-col flex-1 w-full"`.

## Easing
Use a shared constant: `const EXPO_OUT: [number, number, number, number] = [0.16, 1, 0.3, 1];`

## Header (z-50, relative)
- Padding: `clamp(16px, 4vh, 40px) clamp(16px, 3vw, 48px) 0`
- **Logo** (left): Two lines stacked - "CARGOX" in white, "GROUP" in `#ffda00`. Font: `"Barlow Condensed"`, weight 800, size `clamp(22px, min(3.15vh, 2.32vw), 32px)`, line-height 0.9, uppercase, letter-spacing -0.01em. Animates from `opacity:0, y:-20` to visible with EXPO_OUT, duration 0.6.
- **Desktop Nav** (hidden on mobile, flex on md+): Items "Services", "Industries", "Company" each with a chevron-down SVG. Gap: `clamp(20px, 3.8vw, 52px)`. White text, size `clamp(15px, min(1.97vh, 1.45vw), 20px)`, letter-spacing -0.02em. Each item fades in staggered. On hover: color shifts to `#ffda00` with `x: 2`.
- **Mobile Hamburger** (md:hidden): lucide-react `Menu`/`X` icon, white, size 28, toggles a mobile menu overlay.

## Mobile Menu Overlay
- Absolute `inset-0`, z-40, centered flex column, bg `#6682c2`
- Same nav items as buttons, font-size 24px, white, staggered fade-in

## Main Content (z-10, relative)
- `flex-1`, grid: 1 col on mobile, `grid-cols-[2.17fr_1fr]` on lg+
- Padding: `clamp(24px, 8vh, 120px) clamp(16px, 3vw, 48px) 0`
- Gap: `clamp(20px, 4vh, 48px)`

### Left Column - Giant Headline
- Container: `overflow: clip`
- Font: `"Barlow Condensed"`, weight 800, size `clamp(86px, min(14vh, 11vw), 220px)`, line-height 0.78, uppercase, letter-spacing -0.01em
- Three lines with slide-in animations:
  1. "BEYOND" - white, slides from `x: -900` with duration 0.85, delay 0
  2. "BORDERS" - color `#002a35`, `marginLeft: 0.524em`, slides from `x: 900` with duration 0.85, delay 0.13
  3. "AND LIMITS" - white, slides from `x: -900` with duration 0.85, delay 0.26
- All use EXPO_OUT easing

### Right Column
- Flex column, gap: `clamp(16px, 2.66vh, 32px)`

#### Tagline Text
- Font: Helvetica, size `clamp(24px, min(4vh, 3vw), 52px)`, line-height 0.9, letter-spacing -0.02em, color `#002a35`
- Three lines with word-by-word reveal animation (each word slides up from `y:'100%'` with rotateX 45deg):
  1. "Logistics" - marginLeft 0, delay 0.3
  2. "shaped by scale" - marginLeft 1.5em, delay 0.5
  3. "powered by precision" - marginLeft 0, delay 0.7
- Each word has 0.08s stagger, duration 0.6, easing `[0.16, 1, 0.3, 1]`

#### Map Section
- Container: relative, `aspectRatio: '435 / 263'`
- **Map image**: absolute, inset-0, object-contain
  - URL: `https://meez.design/web/media/ext/f9ce5f887859208d.png`

- **Route Lines SVG Overlay**: absolute, pointer-events-none, positioned at `left: 13.8%`, `top: 24.3%`, `width: 68.7%`, aspectRatio `299/143`
  - SVG viewBox: `0 0 299.037 142.509`, overflow visible
  - 4 animated bezier curve paths in `#FFDA00`, strokeWidth 2.5:
    ```
    M128.161 74.6764C79.9989 130.001 71.9994 46.0005 20.9815 111.737
    M216.999 9.99985C260.499 12.4998 222.499 71.9998 291.999 58.9998
    M130.102 70.9998C144.499 -32.0002 183.852 70.2739 219.999 3.99985
    M14.4999 16.9998C111 20.9998 -53.0003 73.4998 21.4999 107
    ```
  - Each path animates `pathLength: 0->1` with duration 1.1, staggered delay starting at 0.55 + i*0.12
  - Animated arrow polygons (triangles `0,-4 8,0 0,4`) move along each path using `<animateMotion>` with `rotate="auto"`, duration `2.5 + i*0.3`s, infinite repeat
  - 5 stop dots at coordinates: `[9.519, 15.519]`, `[289.519, 59.518]`, `[220.519, 9.519]`, `[125.518, 78.519]`, `[19.519, 104.519]`. Each is a yellow circle (r=9.519, fill `#FFDA00`) with a smaller dark center circle (r=3.389, fill `#002A35`). Spring animation with stiffness 420, damping 14.

- **Transport Icons**: 3 circular white icons absolutely positioned on the map:
  - Ship: `left: 26.0%, top: 28.9%`, delay 2.1, URL: `https://meez.design/web/media/ext/0d3cbcc042a65ea1.png`
  - Car: `left: 70.8%, top: 15.6%`, delay 2.2, rotate `9.73deg`, URL: `https://meez.design/web/media/ext/457552dcad941164.png`
  - Plane: `left: 55.2%, top: 52.1%`, delay 2.3, rotate `180deg scaleY(-1)`, URL: `https://meez.design/web/media/ext/c4fe9416e8e5502f.png`
  - Each icon: `width: 14.9%`, aspect-ratio 1, rounded-full, bg-white, box-shadow `0 4px 12px rgba(0,0,0,0.15)`. On hover: scale 1.12, translateY -4px, enhanced shadow. Spring animation: stiffness 220, damping 16.

- **Map description text**: absolute, hidden on mobile (`hidden sm:block`), positioned `left: 55.6%, top: 89%, width: 44%`. Text: "We ensure full transparency at every stage to build trust and drive results." Size `clamp(12px, min(1.6vh, 1.2vw), 20px)`, color `#002a35`, fades in at delay 2.4.

## Footer (z-10, relative)
- Flex row (column on mobile), space-between, padding: `clamp(12px, 3vh, 32px) clamp(16px, 3vw, 48px) clamp(16px, 5vh, 66px)`

### Left - Stat Block
- Animates from `opacity:0, y:24` with delay 0.45, duration 0.65, EXPO_OUT
- "3M+" in `"Barlow Condensed"` weight 800, size `clamp(52px, min(8vh, 6vw), 98px)`, color `#ffda00`, uppercase
- Description: "tons of cargo / successfully delivered / without delays" - size `clamp(16px, min(1.6vh, 1.2vw), 20px)`, white, line-height 1.25
- Small cargo icon in white circle: `clamp(40px, min(5.5vh, 4vw), 67px)` diameter, URL: `https://meez.design/web/media/ext/962814ac70117210.png`

### Right - CTA Button
- Custom SVG pill shape with a circle cutout on the right. Fill `#ffda00`. The full SVG path:
  ```
  M316 0C329.08 0 340.435 7.38674 346.121 18.2162C348.618 22.9736 353.086 26.8535 358.459 26.8535H359.252C364.667 26.8535 369.155 22.9169 371.63 18.1007C377.159 7.34039 388.205 0.00015843 400.931 0C419.195 0 434.001 15.1191 434.001 33.7695L433.99 34.6416C433.537 52.8891 418.909 67.5391 400.931 67.5391C387.96 67.5389 376.734 59.9132 371.317 48.8128C368.923 43.9077 364.427 39.873 358.969 39.873C353.492 39.873 348.986 43.9356 346.589 48.8605C341.074 60.1913 329.449 68 316 68H34.001C15.2233 68 0 52.7777 0 34C0 15.2223 15.2233 0 34.001 0H316ZM400.931 2.44141C384.063 2.44163 370.303 16.419 370.303 33.7695C370.303 51.1201 384.063 65.0974 400.931 65.0977C417.798 65.0977 431.56 51.1202 431.56 33.7695C431.56 16.4189 417.798 2.44141 400.931 2.44141Z
  ```
- ViewBox: `0 0 434.001 68`, preserveAspectRatio `none`
- Size: full-width on mobile (h-56px), on sm+: `h-[clamp(48px,min(6vh,4.5vw),68px)]` with `aspect-[434/68]`
- **Arrow** in the circle cutout: SVG arrow (`viewBox="0 0 16.89 20.37"`, white stroke, strokeWidth 2.2) that rotates from `-135deg` to `-90deg` on hover with 0.35s transition
- **Label**: "Get in touch", centered in the pill area (excluding circle), color `#002a35`, size `clamp(14px, min(1.6vh, 1.2vw), 20px)`
- Animates in from `opacity:0, x:60` with delay 0.5. whileHover: scale 1.08, y:-2. whileTap: scale 0.97.

## Color Palette
- Primary dark: `#002a35`
- White: `#ffffff`
- Accent yellow: `#ffda00`
- Fallback bg: `#1a1a2e`
- Mobile menu bg: `#6682c2`

## Key Behaviors
1. All animations are gated behind `videoReady` state - nothing animates until the video fires `onCanPlay`
2. The entire content fades in once the video is ready
3. All content (header, main, footer) uses `relative z-10` or `z-50` to layer above the video (z-0)
4. Fully responsive: single column on mobile, 2-column grid on lg+
5. Mobile hamburger menu with overlay on md breakpoint

### Source Code
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>CARGOX Group - Beyond Borders and Limits</title>
  <link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@800&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    html, body { height: 100%; overflow: hidden; }
    body { font-family: Helvetica, Arial, sans-serif; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }

    .hero-wrapper {
      width: 100%;
      display: flex;
      flex-direction: column;
      position: relative;
      min-height: 100vh;
      overflow: hidden;
      font-family: Helvetica, Arial, sans-serif;
      background-color: #1a1a2e;
    }

    .video-bg {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      z-index: 0;
    }

    .content-wrapper {
      display: flex;
      flex-direction: column;
      flex: 1;
      width: 100%;
      opacity: 0;
      transition: opacity 0.3s ease;
    }
    .content-wrapper.visible { opacity: 1; }

    /* Header */
    .header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-shrink: 0;
      position: relative;
      z-index: 50;
      padding: clamp(16px, 4vh, 40px) clamp(16px, 3vw, 48px) 0;
    }

    .logo {
      font-family: "Barlow Condensed", sans-serif;
      font-weight: 800;
      font-size: clamp(22px, min(3.15vh, 2.32vw), 32px);
      line-height: 0.9;
      letter-spacing: -0.01em;
      text-transform: uppercase;
      opacity: 0;
      transform: translateY(-20px);
      transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1), transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .logo.animate { opacity: 1; transform: translateY(0); }
    .logo-white { color: #ffffff; }
    .logo-yellow { color: #ffda00; }

    .nav {
      display: flex;
      align-items: center;
      gap: clamp(20px, 3.8vw, 52px);
      opacity: 0;
      transform: translateY(-20px);
      transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1) 0.08s, transform 0.6s cubic-bezier(0.16, 1, 0.3, 1) 0.08s;
    }
    .nav.animate { opacity: 1; transform: translateY(0); }

    .nav-item {
      display: flex;
      align-items: center;
      gap: 4px;
      background: transparent;
      border: none;
      cursor: pointer;
      color: #ffffff;
      font-size: clamp(15px, min(1.97vh, 1.45vw), 20px);
      letter-spacing: -0.02em;
      font-family: Helvetica, Arial, sans-serif;
      opacity: 0;
      transition: opacity 0.4s ease, color 0.1s ease, transform 0.1s ease;
    }
    .nav-item.animate { opacity: 1; }
    .nav-item:hover { color: #ffda00; transform: translateX(2px); }
    .nav-item svg { width: 0.9em; height: 0.9em; }

    .hamburger {
      display: none;
      align-items: center;
      justify-content: center;
      background: transparent;
      border: none;
      cursor: pointer;
      color: #ffffff;
      width: 40px;
      height: 40px;
    }

    /* Main */
    .main-content {
      flex: 1;
      overflow: hidden;
      display: grid;
      grid-template-columns: 2.17fr 1fr;
      position: relative;
      z-index: 10;
      padding: clamp(24px, 8vh, 120px) clamp(16px, 3vw, 48px) 0;
      gap: clamp(20px, 4vh, 48px);
    }

    /* Headline */
    .headline-container { overflow: clip; }
    .headline {
      font-family: "Barlow Condensed", sans-serif;
      font-weight: 800;
      font-size: clamp(86px, min(14vh, 11vw), 220px);
      line-height: 0.78;
      letter-spacing: -0.01em;
      text-transform: uppercase;
    }
    .headline-line {
      opacity: 0;
      transition: transform 0.85s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.85s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .headline-line.line-1 { color: #ffffff; transform: translateX(-900px); }
    .headline-line.line-2 { color: #002a35; margin-left: 0.524em; transform: translateX(900px); }
    .headline-line.line-3 { color: #ffffff; transform: translateX(-900px); }
    .headline-line.animate { opacity: 1; transform: translateX(0); }

    /* Right column */
    .right-col {
      display: flex;
      flex-direction: column;
      gap: clamp(16px, 2.66vh, 32px);
    }

    /* Tagline */
    .tagline {
      font-family: Helvetica, Arial, sans-serif;
      font-size: clamp(24px, min(4vh, 3vw), 52px);
      line-height: 0.9;
      letter-spacing: -0.02em;
      color: #002a35;
    }
    .tagline-line { white-space: nowrap; overflow: visible; }
    .tagline-line + .tagline-line { margin-top: 0.3em; }
    .tagline-line-2 { margin-left: 1.5em; }

    .tagline-word {
      display: inline-block;
      margin-right: 0.25em;
      opacity: 0;
      transform: translateY(100%) perspective(600px) rotateX(45deg);
      transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .tagline-word.animate { opacity: 1; transform: translateY(0) perspective(600px) rotateX(0deg); }

    /* Map */
    .map-container { position: relative; width: 100%; aspect-ratio: 435 / 263; }
    .map-img { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: contain; }

    .routes-overlay {
      position: absolute;
      pointer-events: none;
      left: 13.8%;
      top: 24.3%;
      width: 68.7%;
      aspect-ratio: 299 / 143;
    }
    .routes-svg { width: 100%; height: 100%; overflow: visible; }

    .route-path {
      stroke: #FFDA00;
      stroke-width: 2.5;
      fill: none;
      stroke-dasharray: 1000;
      stroke-dashoffset: 1000;
      opacity: 0;
    }
    .route-path.animate { opacity: 1; animation: drawPath 1.1s ease-in-out forwards; }
    @keyframes drawPath { to { stroke-dashoffset: 0; } }

    .transport-icon {
      position: absolute;
      width: 14.9%;
      aspect-ratio: 1;
      border-radius: 50%;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      transform: scale(0);
      opacity: 0;
      transition: transform 0.5s cubic-bezier(0.34, 1.56, 0.64, 1), opacity 0.3s ease, box-shadow 0.2s ease;
    }
    .transport-icon.animate { transform: scale(1); opacity: 1; }
    .transport-icon:hover { transform: scale(1.12) translateY(-4px) !important; box-shadow: 0 8px 24px rgba(0,0,0,0.25); }
    .transport-icon img { width: 80%; height: 80%; object-fit: cover; }

    .stop-dot { transform-box: fill-box; transform-origin: center; transform: scale(0); }
    .stop-dot.animate { animation: popIn 0.4s cubic-bezier(0.34, 1.56, 0.64, 1) forwards; }
    @keyframes popIn { to { transform: scale(1); } }

    .map-desc {
      position: absolute;
      left: 55.6%;
      top: 89%;
      width: 44%;
      font-family: Helvetica, Arial, sans-serif;
      font-size: clamp(12px, min(1.6vh, 1.2vw), 20px);
      line-height: 1.25;
      letter-spacing: -0.02em;
      color: #002a35;
      opacity: 0;
      transition: opacity 0.6s ease;
    }
    .map-desc.animate { opacity: 1; }

    /* Footer */
    .footer {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-shrink: 0;
      position: relative;
      z-index: 10;
      padding: clamp(12px, 3vh, 32px) clamp(16px, 3vw, 48px) clamp(16px, 5vh, 66px);
    }

    .stat-block {
      display: flex;
      align-items: center;
      gap: 0.9em;
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.65s cubic-bezier(0.16, 1, 0.3, 1), transform 0.65s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .stat-block.animate { opacity: 1; transform: translateY(0); }

    .stat-number {
      font-family: "Barlow Condensed", sans-serif;
      font-weight: 800;
      font-size: clamp(52px, min(8vh, 6vw), 98px);
      line-height: 1;
      color: #ffda00;
      text-transform: uppercase;
      letter-spacing: -0.01em;
    }
    .stat-text {
      font-size: clamp(16px, min(1.6vh, 1.2vw), 20px);
      line-height: 1.25;
      letter-spacing: -0.02em;
      color: #ffffff;
    }
    .stat-icon {
      position: relative;
      flex-shrink: 0;
      border-radius: 50%;
      background: white;
      overflow: hidden;
      width: clamp(40px, min(5.5vh, 4vw), 67px);
      aspect-ratio: 1;
    }
    .stat-icon img { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: contain; padding: 10%; }

    /* CTA */
    .cta-btn {
      position: relative;
      cursor: pointer;
      border: none;
      background: transparent;
      padding: 0;
      height: clamp(48px, min(6vh, 4.5vw), 68px);
      aspect-ratio: 434 / 68;
      opacity: 0;
      transform: translateX(60px);
      transition: opacity 0.7s cubic-bezier(0.16, 1, 0.3, 1), transform 0.7s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .cta-btn.animate { opacity: 1; transform: translateX(0); }
    .cta-btn:hover { transform: scale(1.08) translateY(-2px); }
    .cta-btn:active { transform: scale(0.97) translateY(0); }
    .cta-btn svg.cta-shape { position: absolute; inset: 0; width: 100%; height: 100%; }

    .cta-arrow-wrap {
      position: absolute;
      right: 0;
      top: 3.59%;
      width: clamp(42px, 14.43%, 62px);
      height: 92.15%;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .cta-arrow {
      width: 40%;
      transform: rotate(-135deg);
      transition: transform 0.35s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    }
    .cta-btn:hover .cta-arrow { transform: rotate(-90deg); }

    .cta-label {
      position: absolute;
      left: 0;
      right: 14.43%;
      top: 50%;
      transform: translateY(-50%);
      text-align: center;
      font-family: Helvetica, Arial, sans-serif;
      font-size: clamp(14px, min(1.6vh, 1.2vw), 20px);
      color: #002a35;
      letter-spacing: 0.01em;
      white-space: nowrap;
      pointer-events: none;
    }

    /* Mobile */
    @media (max-width: 767px) {
      .nav { display: none !important; }
      .hamburger { display: flex; }
      .main-content { grid-template-columns: 1fr; }
      .footer { flex-direction: column; gap: 16px; }
      .cta-btn { width: 100%; height: 56px; aspect-ratio: unset; }
      .map-desc { display: none; }
    }
    @media (min-width: 768px) {
      .hamburger { display: none; }
    }

    /* Mobile overlay */
    .mobile-overlay {
      display: none;
      position: absolute;
      inset: 0;
      z-index: 40;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background-color: #6682c2;
    }
    .mobile-overlay.open { display: flex; }
    .mobile-overlay button {
      background: transparent;
      border: none;
      cursor: pointer;
      padding: 16px;
      color: #ffffff;
      font-size: 24px;
      letter-spacing: -0.02em;
      font-family: Helvetica, Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="hero-wrapper">
    <video class="video-bg" autoplay muted loop playsinline id="bgVideo"
      src="https://meez.design/web/media/ext/597d53d9b15f2d2d.mp4">
    </video>

    <div class="content-wrapper" id="contentWrapper">
      <!-- Header -->
      <header class="header">
        <div class="logo" id="logo">
          <div class="logo-white">CARGOX</div>
          <div class="logo-yellow">GROUP</div>
        </div>

        <nav class="nav" id="nav">
          <button class="nav-item" style="transition-delay: 0.1s">
            Services
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none"><path d="M6 9L12 15L18 9" stroke="currentColor" stroke-width="1.5" stroke-linecap="square" stroke-linejoin="round"/></svg>
          </button>
          <button class="nav-item" style="transition-delay: 0.16s">
            Industries
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none"><path d="M6 9L12 15L18 9" stroke="currentColor" stroke-width="1.5" stroke-linecap="square" stroke-linejoin="round"/></svg>
          </button>
          <button class="nav-item" style="transition-delay: 0.22s">
            Company
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none"><path d="M6 9L12 15L18 9" stroke="currentColor" stroke-width="1.5" stroke-linecap="square" stroke-linejoin="round"/></svg>
          </button>
        </nav>

        <button class="hamburger" id="hamburgerBtn">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/></svg>
        </button>
      </header>

      <!-- Mobile overlay -->
      <div class="mobile-overlay" id="mobileOverlay">
        <button>Services</button>
        <button>Industries</button>
        <button>Company</button>
      </div>

      <!-- Main -->
      <main class="main-content">
        <!-- Left headline -->
        <div class="headline-container">
          <div class="headline">
            <div class="headline-line line-1" id="hl1">BEYOND</div>
            <div class="headline-line line-2" id="hl2">BORDERS</div>
            <div class="headline-line line-3" id="hl3">AND LIMITS</div>
          </div>
        </div>

        <!-- Right column -->
        <div class="right-col">
          <!-- Tagline -->
          <div class="tagline">
            <div class="tagline-line">
              <span class="tagline-word" style="transition-delay: 0.3s">Logistics</span>
            </div>
            <div class="tagline-line tagline-line-2">
              <span class="tagline-word" style="transition-delay: 0.5s">shaped</span>
              <span class="tagline-word" style="transition-delay: 0.58s">by</span>
              <span class="tagline-word" style="transition-delay: 0.66s">scale</span>
            </div>
            <div class="tagline-line">
              <span class="tagline-word" style="transition-delay: 0.7s">powered</span>
              <span class="tagline-word" style="transition-delay: 0.78s">by</span>
              <span class="tagline-word" style="transition-delay: 0.86s">precision</span>
            </div>
          </div>

          <!-- Map -->
          <div class="map-container">
            <img class="map-img" src="https://meez.design/web/media/ext/f9ce5f887859208d.png" alt="World map" />

            <!-- Route lines -->
            <div class="routes-overlay">
              <svg class="routes-svg" viewBox="0 0 299.037 142.509" fill="none">
                <!-- Path 1 -->
                <path class="route-path" id="rp0" d="M128.161 74.6764C79.9989 130.001 71.9994 46.0005 20.9815 111.737"/>
                <!-- Path 2 -->
                <path class="route-path" id="rp1" d="M216.999 9.99985C260.499 12.4998 222.499 71.9998 291.999 58.9998"/>
                <!-- Path 3 -->
                <path class="route-path" id="rp2" d="M130.102 70.9998C144.499 -32.0002 183.852 70.2739 219.999 3.99985"/>
                <!-- Path 4 -->
                <path class="route-path" id="rp3" d="M14.4999 16.9998C111 20.9998 -53.0003 73.4998 21.4999 107"/>

                <!-- Animated arrows -->
                <g id="arrows" style="opacity: 0">
                  <polygon points="0,-4 8,0 0,4" fill="#FFDA00">
                    <animateMotion dur="2.5s" repeatCount="indefinite" rotate="auto" path="M128.161 74.6764C79.9989 130.001 71.9994 46.0005 20.9815 111.737"/>
                  </polygon>
                  <polygon points="0,-4 8,0 0,4" fill="#FFDA00">
                    <animateMotion dur="2.8s" repeatCount="indefinite" rotate="auto" path="M216.999 9.99985C260.499 12.4998 222.499 71.9998 291.999 58.9998"/>
                  </polygon>
                  <polygon points="0,-4 8,0 0,4" fill="#FFDA00">
                    <animateMotion dur="3.1s" repeatCount="indefinite" rotate="auto" path="M130.102 70.9998C144.499 -32.0002 183.852 70.2739 219.999 3.99985"/>
                  </polygon>
                  <polygon points="0,-4 8,0 0,4" fill="#FFDA00">
                    <animateMotion dur="3.4s" repeatCount="indefinite" rotate="auto" path="M14.4999 16.9998C111 20.9998 -53.0003 73.4998 21.4999 107"/>
                  </polygon>
                </g>

                <!-- Stop dots -->
                <circle class="stop-dot" id="sd0" cx="9.519" cy="15.519" r="9.519" fill="#FFDA00"/>
                <circle class="stop-dot" id="sd0i" cx="9.447" cy="15.447" r="3.389" fill="#002A35"/>
                <circle class="stop-dot" id="sd1" cx="289.519" cy="59.518" r="9.519" fill="#FFDA00"/>
                <circle class="stop-dot" id="sd1i" cx="289.447" cy="59.446" r="3.389" fill="#002A35"/>
                <circle class="stop-dot" id="sd2" cx="220.519" cy="9.519" r="9.519" fill="#FFDA00"/>
                <circle class="stop-dot" id="sd2i" cx="220.447" cy="9.447" r="3.389" fill="#002A35"/>
                <circle class="stop-dot" id="sd3" cx="125.518" cy="78.519" r="9.519" fill="#FFDA00"/>
                <circle class="stop-dot" id="sd3i" cx="125.446" cy="78.447" r="3.389" fill="#002A35"/>
                <circle class="stop-dot" id="sd4" cx="19.519" cy="104.519" r="9.519" fill="#FFDA00"/>
                <circle class="stop-dot" id="sd4i" cx="19.447" cy="104.447" r="3.389" fill="#002A35"/>
              </svg>
            </div>

            <!-- Transport icons -->
            <div class="transport-icon" id="ti0" style="left: 26.0%; top: 28.9%;">
              <img src="https://meez.design/web/media/ext/0d3cbcc042a65ea1.png" alt="Ship"/>
            </div>
            <div class="transport-icon" id="ti1" style="left: 70.8%; top: 15.6%;">
              <img src="https://meez.design/web/media/ext/457552dcad941164.png" alt="Car" style="transform: rotate(9.73deg)"/>
            </div>
            <div class="transport-icon" id="ti2" style="left: 55.2%; top: 52.1%;">
              <img src="https://meez.design/web/media/ext/c4fe9416e8e5502f.png" alt="Plane" style="transform: rotate(180deg) scaleY(-1)"/>
            </div>

            <!-- Map description -->
            <p class="map-desc" id="mapDesc">We ensure full transparency at every stage to build trust and drive results.</p>
          </div>
        </div>
      </main>

      <!-- Footer -->
      <footer class="footer">
        <div class="stat-block" id="statBlock">
          <div class="stat-number">3M+</div>
          <div class="stat-text">
            <div>tons of cargo</div>
            <div>successfully delivered</div>
            <div>without delays</div>
          </div>
          <div class="stat-icon">
            <img src="https://meez.design/web/media/ext/962814ac70117210.png" alt="Cargo"/>
          </div>
        </div>

        <button class="cta-btn" id="ctaBtn">
          <svg class="cta-shape" viewBox="0 0 434.001 68" preserveAspectRatio="none" fill="#ffda00" fill-rule="evenodd">
            <path d="M316 0C329.08 0 340.435 7.38674 346.121 18.2162C348.618 22.9736 353.086 26.8535 358.459 26.8535H359.252C364.667 26.8535 369.155 22.9169 371.63 18.1007C377.159 7.34039 388.205 0.00015843 400.931 0C419.195 0 434.001 15.1191 434.001 33.7695L433.99 34.6416C433.537 52.8891 418.909 67.5391 400.931 67.5391C387.96 67.5389 376.734 59.9132 371.317 48.8128C368.923 43.9077 364.427 39.873 358.969 39.873C353.492 39.873 348.986 43.9356 346.589 48.8605C341.074 60.1913 329.449 68 316 68H34.001C15.2233 68 0 52.7777 0 34C0 15.2223 15.2233 0 34.001 0H316ZM400.931 2.44141C384.063 2.44163 370.303 16.419 370.303 33.7695C370.303 51.1201 384.063 65.0974 400.931 65.0977C417.798 65.0977 431.56 51.1202 431.56 33.7695C431.56 16.4189 417.798 2.44141 400.931 2.44141Z"/>
          </svg>
          <div class="cta-arrow-wrap">
            <svg class="cta-arrow" viewBox="0 0 16.89 20.37" fill="none">
              <path d="M8.44473 1.0994V18.8164M1.55479 11.9264L8.44473 18.8164L15.3347 11.9264" stroke="white" stroke-linecap="square" stroke-width="2.2"/>
            </svg>
          </div>
          <span class="cta-label">Get in touch</span>
        </button>
      </footer>
    </div>
  </div>

  <script>
    const video = document.getElementById('bgVideo');
    const content = document.getElementById('contentWrapper');

    function initAnimations() {
      content.classList.add('visible');

      // Header
      setTimeout(() => document.getElementById('logo').classList.add('animate'), 0);
      setTimeout(() => document.getElementById('nav').classList.add('animate'), 80);
      document.querySelectorAll('.nav-item').forEach((item, i) => {
        setTimeout(() => item.classList.add('animate'), 100 + i * 60);
      });

      // Headlines
      setTimeout(() => document.getElementById('hl1').classList.add('animate'), 0);
      setTimeout(() => document.getElementById('hl2').classList.add('animate'), 130);
      setTimeout(() => document.getElementById('hl3').classList.add('animate'), 260);

      // Tagline words
      document.querySelectorAll('.tagline-word').forEach(word => {
        const delay = parseFloat(word.style.transitionDelay) * 1000;
        setTimeout(() => word.classList.add('animate'), delay);
      });

      // Route paths
      const paths = document.querySelectorAll('.route-path');
      paths.forEach((path, i) => {
        const len = path.getTotalLength();
        path.style.strokeDasharray = len;
        path.style.strokeDashoffset = len;
        setTimeout(() => {
          path.classList.add('animate');
          path.style.strokeDashoffset = '0';
          path.style.transition = `stroke-dashoffset 1.1s ease-in-out, opacity 0.01s`;
        }, 550 + i * 120);
      });

      // Arrows
      setTimeout(() => document.getElementById('arrows').style.opacity = '1', 1600);

      // Stop dots
      for (let i = 0; i < 5; i++) {
        setTimeout(() => {
          document.getElementById('sd' + i).classList.add('animate');
        }, 1650 + i * 90);
        setTimeout(() => {
          document.getElementById('sd' + i + 'i').classList.add('animate');
        }, 1720 + i * 90);
      }

      // Transport icons
      setTimeout(() => document.getElementById('ti0').classList.add('animate'), 2100);
      setTimeout(() => document.getElementById('ti1').classList.add('animate'), 2200);
      setTimeout(() => document.getElementById('ti2').classList.add('animate'), 2300);

      // Map description
      setTimeout(() => document.getElementById('mapDesc').classList.add('animate'), 2400);

      // Footer
      setTimeout(() => document.getElementById('statBlock').classList.add('animate'), 450);
      setTimeout(() => document.getElementById('ctaBtn').classList.add('animate'), 500);
    }

    video.addEventListener('canplay', function handler() {
      video.removeEventListener('canplay', handler);
      initAnimations();
    });

    // Fallback if video is already cached
    if (video.readyState >= 3) {
      initAnimations();
    }

    // Mobile menu toggle
    const hamburgerBtn = document.getElementById('hamburgerBtn');
    const mobileOverlay = document.getElementById('mobileOverlay');
    hamburgerBtn.addEventListener('click', () => {
      mobileOverlay.classList.toggle('open');
    });
  </script>
</body>
</html>
````
