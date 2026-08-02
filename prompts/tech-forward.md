# Tech-Forward

**Category:** Hero · **Source:** https://meez.design/p/tech-forward · **License:** free to use, commercial projects OK

Copy everything inside the fence and paste it into Lovable, Bolt, v0, Cursor or Claude Code — don't trim it; the detail is the point.

````
Create a full-screen hero section landing page using React, Vite, and Framer Motion (`motion` package). Use plain CSS (no Tailwind). The font is Inter (weights 300, 400, 500, 600) from Google Fonts. The design is minimal black-and-white with a full-viewport background video.

**Stack:** React 19, Vite, `motion` (framer-motion), `lucide-react` (for the Plus icon).

**Layout:**
- Full viewport height (`min-height: 100vh`), white background, flex column with `justify-content: space-between`
- Fixed navbar at top (z-index 50, pointer-events none on the nav itself, auto on children)
- Absolutely positioned full-screen video behind everything (z-index 0)
- Footer content pinned to bottom (z-index 30) with a white gradient fade-up background

**Navbar (fixed, top):**
- Left side contains:
  1. Logo: custom SVG icon (two rotated rounded rectangles at -35deg, black fill) + brand text "NeuralKinetics" (hidden on mobile, shown on desktop 768px+)
  2. Menu button: black pill with white circle containing a Plus icon (lucide, size 12, strokeWidth 3) + "Menu" text (11px, white)
  3. Tags pill: light gray (#F4F4F6) rounded-full container with two text labels "Advanced Bionics" and "Cognitive AI" (hidden on mobile, shown on desktop)
- Right side contains:
  - A light gray pill with a black circle button (containing a 4-dot grid SVG icon) + label "Adaptive Systems" (hidden on mobile)

**Background Video:**
- URL: `https://meez.design/web/media/ext/a9e8d581015638ec.mp4`
- autoPlay, muted, playsInline, object-fit: cover
- On mobile: video wrapper is 80% width and 80% height (centered)
- On desktop (768px+): video wrapper is 100% width and 100% height

**Footer content (bottom, over gradient):**
- Background: `linear-gradient(to top, #ffffff 0%, rgba(255,255,255,0.8) 50%, transparent 100%)`
- On mobile: stacks vertically. On desktop: row layout, items aligned to bottom.
- Left block:
  1. Subtitle line: small black dot (8px circle) + "Best digital banking card 2026" (13px, 55% opacity black)
  2. Heading: "One Card, Zero / Limits. Worldwide." on two lines. Font-weight 300, clamp(2rem, 8vw, 4.5rem) on mobile, clamp(2.5rem, 5.5vw, 4.5rem) on desktop, letter-spacing -0.03em, line-height 1
  3. Two buttons: "See Features" (black pill, white text, 13px) and "How It Works" (transparent with dark border rgba(0,0,0,0.35), 13px)
- Right block: Three tag pills "Neuromorphic", "AGI", "Cybernetics" (white bg, light border rgba(0,0,0,0.12), 11px, rounded-full)

**Animations (using `motion` from 'motion/react'):**
- Navbar: slides down from y:-16, opacity 0 to visible. Duration 0.8s, ease [0.16, 1, 0.3, 1]
- Video: fades in from opacity 0 + scale 1.05 to opacity 1 + scale 1. Duration 1.8s
- Footer wrapper: slides up from y:20, delay 0.5s, duration 1s
- Subtitle: slides up from y:16, delay 0.6s, duration 0.8s
- Heading: slides up from y:20, delay 0.8s, duration 0.8s
- Buttons: slides up from y:16, delay 1.0s, duration 0.8s
- All use ease: [0.16, 1, 0.3, 1]

**Responsive (mobile-first, breakpoint at 768px):**
- Mobile: navbar padding 16px, smaller buttons (28px circles), brand text hidden, tags hidden, right label hidden, footer stacks vertically, video at 80% size
- Desktop (768px+): navbar padding 24px 32px, larger buttons (32px circles), all text/tags visible, footer is row layout, video fills 100%

### Source Code
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NeuralKinetics Hero</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet" />
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: #fff;
      color: #000;
      font-family: 'Inter', system-ui, -apple-system, sans-serif;
      -webkit-font-smoothing: antialiased;
    }

    ::selection { background: #000; color: #fff; }

    .page {
      position: relative;
      min-height: 100vh;
      width: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      overflow: hidden;
    }

    /* === NAVBAR === */
    .nav-bar {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      padding: 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      z-index: 50;
      pointer-events: none;
      animation: slideDown 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
      opacity: 0;
    }

    @keyframes slideDown {
      from { transform: translateY(-16px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .nav-left {
      display: flex;
      align-items: center;
      gap: 8px;
      pointer-events: auto;
    }

    .nav-logo {
      display: flex;
      align-items: center;
      gap: 4px;
      cursor: pointer;
      padding: 4px 8px;
      border-radius: 8px;
    }

    .nav-logo-text {
      font-weight: 500;
      font-size: 15px;
      letter-spacing: -0.02em;
      color: #000;
      display: none;
    }

    .nav-menu-btn {
      display: flex;
      align-items: center;
      background-color: #000;
      color: #fff;
      border: 1px solid rgba(0,0,0,0.03);
      padding: 4px 16px 4px 4px;
      gap: 8px;
      border-radius: 9999px;
      cursor: pointer;
      font-family: inherit;
    }

    .nav-menu-icon {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background-color: #fff;
      color: #000;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .nav-menu-label {
      font-size: 11px;
      font-weight: 500;
      padding-right: 2px;
    }

    .nav-tags {
      display: none;
      align-items: center;
      background-color: #F4F4F6;
      border: 1px solid rgba(0,0,0,0.03);
      border-radius: 9999px;
      padding: 0 24px;
      height: 40px;
      font-size: 11px;
      font-weight: 400;
      color: rgba(0,0,0,0.55);
      gap: 20px;
      user-select: none;
    }

    .nav-right { pointer-events: auto; }

    .nav-right-pill {
      display: flex;
      align-items: center;
      background-color: #F4F4F6;
      border-radius: 9999px;
      padding: 4px 16px 4px 4px;
      gap: 10px;
      border: 1px solid rgba(0,0,0,0.03);
    }

    .nav-right-icon {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background-color: #000;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      border: none;
      cursor: pointer;
    }

    .nav-right-label {
      font-size: 11px;
      font-weight: 500;
      color: rgba(0,0,0,0.65);
      user-select: none;
      display: none;
    }

    /* === VIDEO === */
    .video-container {
      position: absolute;
      inset: 0;
      z-index: 0;
      pointer-events: none;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .video-wrapper {
      position: relative;
      width: 80%;
      height: 80%;
      animation: videoFadeIn 1.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
      opacity: 0;
    }

    @keyframes videoFadeIn {
      from { opacity: 0; transform: scale(1.05); }
      to { opacity: 1; transform: scale(1); }
    }

    .video-wrapper video {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      pointer-events: none;
    }

    /* === SPACER === */
    .spacer { flex: 1; position: relative; z-index: 10; }

    /* === FOOTER === */
    .bottom-footer {
      width: 100%;
      position: relative;
      z-index: 30;
      padding: 32px 20px 40px;
      background: linear-gradient(to top, #ffffff 0%, rgba(255,255,255,0.8) 50%, transparent 100%);
    }

    .footer-inner {
      width: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: flex-start;
      gap: 24px;
      animation: slideUp 1s cubic-bezier(0.16, 1, 0.3, 1) 0.5s forwards;
      opacity: 0;
    }

    @keyframes slideUp {
      from { transform: translateY(20px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .footer-left {
      display: flex;
      flex-direction: column;
      gap: 20px;
      max-width: 540px;
    }

    .footer-subtitle {
      display: flex;
      align-items: center;
      gap: 8px;
      animation: slideUpSmall 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.6s forwards;
      opacity: 0;
    }

    @keyframes slideUpSmall {
      from { transform: translateY(16px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .footer-subtitle .dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background-color: rgba(0,0,0,0.75);
      flex-shrink: 0;
    }

    .footer-subtitle span {
      font-size: 13px;
      color: rgba(0,0,0,0.55);
    }

    .footer-heading {
      font-size: clamp(2rem, 8vw, 4.5rem);
      font-weight: 300;
      line-height: 1;
      letter-spacing: -0.03em;
      color: #000;
      animation: slideUpMedium 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.8s forwards;
      opacity: 0;
    }

    @keyframes slideUpMedium {
      from { transform: translateY(20px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .footer-buttons {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-top: 4px;
      animation: slideUpSmall 0.8s cubic-bezier(0.16, 1, 0.3, 1) 1.0s forwards;
      opacity: 0;
    }

    .btn-primary {
      padding: 12px 22px;
      background-color: #000;
      color: #fff;
      font-size: 13px;
      font-weight: 500;
      border-radius: 9999px;
      border: none;
      cursor: pointer;
      font-family: inherit;
    }

    .btn-outline {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 12px 22px;
      background-color: transparent;
      border: 1px solid rgba(0,0,0,0.35);
      color: #000;
      font-size: 13px;
      font-weight: 500;
      border-radius: 9999px;
      cursor: pointer;
      font-family: inherit;
    }

    .footer-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      align-items: flex-end;
    }

    .tag-button {
      padding: 10px 18px;
      border: 1px solid rgba(0,0,0,0.12);
      color: #000;
      font-size: 11px;
      font-weight: 400;
      border-radius: 9999px;
      background-color: #fff;
      cursor: pointer;
      font-family: inherit;
    }

    /* === DESKTOP 768px+ === */
    @media (min-width: 768px) {
      .nav-bar { padding: 24px 32px; }
      .nav-left { gap: 12px; }
      .nav-logo-text { display: inline; font-size: 17px; }
      .nav-menu-btn { padding: 4px 20px 4px 4px; gap: 10px; }
      .nav-menu-icon { width: 32px; height: 32px; }
      .nav-tags { display: flex; }
      .nav-right-pill { padding: 4px 24px 4px 4px; gap: 14px; }
      .nav-right-icon { width: 32px; height: 32px; }
      .nav-right-label { display: inline; }
      .video-wrapper { width: 100%; height: 100%; }
      .bottom-footer { padding: 40px 48px 56px; }
      .footer-inner { flex-direction: row; align-items: flex-end; gap: 32px; }
      .footer-left { gap: 24px; }
      .footer-heading { font-size: clamp(2.5rem, 5.5vw, 4.5rem); white-space: nowrap; }
      .btn-primary { padding: 13px 26px; }
      .btn-outline { padding: 13px 26px; }
      .tag-button { padding: 12px 22px; }
    }
  </style>
</head>
<body>
  <div class="page">

    <!-- Navbar -->
    <nav class="nav-bar">
      <div class="nav-left">
        <div class="nav-logo">
          <svg width="36" height="36" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="7" y="19" width="15" height="5.5" rx="2.75" transform="rotate(-35 7 19)" fill="#000"/>
            <rect x="17.5" y="24" width="15" height="5.5" rx="2.75" transform="rotate(-35 17.5 24)" fill="#000"/>
          </svg>
          <span class="nav-logo-text">NeuralKinetics</span>
        </div>

        <button class="nav-menu-btn">
          <div class="nav-menu-icon">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
              <line x1="12" y1="5" x2="12" y2="19"/>
              <line x1="5" y1="12" x2="19" y2="12"/>
            </svg>
          </div>
          <span class="nav-menu-label">Menu</span>
        </button>

        <div class="nav-tags">
          <span>Advanced Bionics</span>
          <span>Cognitive AI</span>
        </div>
      </div>

      <div class="nav-right">
        <div class="nav-right-pill">
          <button class="nav-right-icon">
            <svg width="13" height="13" viewBox="0 0 24 24" fill="none">
              <circle cx="12" cy="5" r="2.2" fill="currentColor"/>
              <circle cx="12" cy="19" r="2.2" fill="currentColor"/>
              <circle cx="5" cy="12" r="2.2" fill="currentColor"/>
              <circle cx="19" cy="12" r="2.2" fill="currentColor"/>
              <path d="M12 7.5v9M7.5 12h9" stroke="currentColor" stroke-width="1.5" opacity="0.6"/>
            </svg>
          </button>
          <span class="nav-right-label">Adaptive Systems</span>
        </div>
      </div>
    </nav>

    <!-- Background Video -->
    <div class="video-container">
      <div class="video-wrapper">
        <video
          src="https://meez.design/web/media/ext/a9e8d581015638ec.mp4"
          autoplay
          muted
          playsinline
        ></video>
      </div>
    </div>

    <!-- Spacer -->
    <main class="spacer"></main>

    <!-- Footer Content -->
    <footer class="bottom-footer">
      <div class="footer-inner">
        <div class="footer-left">
          <div class="footer-subtitle">
            <div class="dot"></div>
            <span>Best digital banking card 2026</span>
          </div>

          <h2 class="footer-heading">
            <div>One Card, Zero</div>
            <div>Limits. Worldwide.</div>
          </h2>

          <div class="footer-buttons">
            <button class="btn-primary">See Features</button>
            <button class="btn-outline">How It Works</button>
          </div>
        </div>

        <div class="footer-tags">
          <button class="tag-button">Neuromorphic</button>
          <button class="tag-button">AGI</button>
          <button class="tag-button">Cybernetics</button>
        </div>
      </div>
    </footer>
  </div>
</body>
</html>
````
