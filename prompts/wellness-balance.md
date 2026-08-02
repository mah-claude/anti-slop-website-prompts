# Wellness Balance

**Category:** Hero · **Source:** https://meez.design/p/wellness-balance · **License:** free to use, commercial projects OK

Copy everything inside the fence and paste it into Lovable, Bolt, v0, Cursor or Claude Code — don't trim it; the detail is the point.

````
Create a single-page hero landing for a wellness/supplements brand called "TerraElix" using React + Tailwind CSS + Lucide React icons. The page is a full-viewport hero with a background image, navbar, headline with word-by-word reveal animations, CTA section, and a 3-panel footer strip. It must be fully responsive (mobile, tablet, desktop).

---

## Fonts

Import from Google Fonts:
- **DM Sans** (weights 400, 500) -- used for brand name, nav links, headline, panel 1 text
- **Inter** (weights 400, 500) -- used for buttons, body text, panel 2/3 text

---

## Background

Full-screen background image covering the entire viewport:
```
url: https://meez.design/web/media/ext/4dfc1a4b05bd693d.webp
background-size: cover; background-position: center; background-repeat: no-repeat;
```

---

## Layout Structure

```
<div> (min-h-screen, flex flex-col, relative, overflow-hidden)
  <nav> -- navbar
  <section> -- hero content (flex-1, flex col, justify-center)
  <div> -- mobile/tablet product image (visible below lg)
  <div> -- 3-panel grid footer
  <img> -- desktop floating product image (absolute, hidden below lg)
</div>
```

---

## Navbar

- **Left:** Brand name "TerraElix" -- white, DM Sans 500, 30px, letter-spacing -0.05em
- **Center (desktop only, hidden on mobile):** Nav links "About", "Products", "Promotions", "Contact" -- DM Sans 500, 18px, text-white/90, gap 10 (lg)
- **Right:** Row of icon buttons + avatar + mobile menu toggle
  - Search icon (Lucide `Search`, size 20, strokeWidth 1.5)
  - Shopping bag icon (Lucide `ShoppingBag`, size 20, strokeWidth 1.5)
  - Return icon (Lucide `CornerUpLeft`, size 20, strokeWidth 1.5)
  - Round avatar image (w-8 h-8, lg:w-10 lg:h-10, rounded-full, object-cover):
    ```
    https://meez.design/web/media/ext/933e27c46b639e84.png
    ```
  - Hamburger menu button (md:hidden, Lucide `Menu` / `X` toggle)

- **Mobile overlay menu:** fixed inset-0 bg-black/90 z-30 with centered nav links (text-2xl, white)

Padding: px-5 sm:px-8 lg:px-10, py-4 lg:py-5

---

## Hero Headline

Font: DM Sans, weight 400, letter-spacing -0.05em

Responsive sizes:
- Base: 48px/50px line-height
- sm: 80px/72px
- md: 110px/95px
- lg: 130px/110px
- xl: 155px/125px

Text layout (3 lines):
```
Line 1: "The" (white) "Power" (white) "of" (white/45 -- dimmed)
Line 2: "Nature" (dimmed) "in" (dimmed) "Every" (white)
Line 3: "Capsule" (white) + inline image
```

Each word is wrapped in a container with overflow-hidden, and the inner span animates with `wordReveal` (translateY 100% + blur to visible). Staggered delays: 0.3s, 0.4s, 0.5s, 0.6s, 0.7s, 0.8s, 0.9s.

**Inline image** after "Capsule" (hidden on mobile, sm:inline-block, align-middle, ml-2 lg:ml-4):
```
https://meez.design/web/media/ext/014f4c2bed24ce90.png
height: clamp(60px, 10vw, 160px); width: auto;
```

---

## CTA Section

Below the headline, mt-8 sm:mt-12 lg:mt-[75px]. Flex row on sm+, column on mobile. Gap: 5 (mobile), 8 (sm), 50px (lg).

- **Button:** "Explore Now" + ArrowUpRight icon. bg-black text-white rounded-md. Sizes: w-full sm:w-[240px] md:w-[280px] lg:w-[310px], h-14 sm:h-16 lg:h-[72px]. Font: Inter 500, responsive text (base to 2xl), letter-spacing -0.03em.
- **Paragraph:** "Discover our new plant-based supplements for daily balance and clean energy." -- white, max-w-[310px], Inter 400, text-sm sm:text-base lg:text-lg, line-height 1.45, letter-spacing -0.03em.

---

## Mobile/Tablet Product Image (lg:hidden)

Visible below lg breakpoint. Oversized, bleeding off edges:
```
https://meez.design/web/media/ext/8f861b7c00ec34fe.png
w-[180%] sm:w-[151%] max-w-[1296px], object-contain, mx-auto, drop-shadow-2xl
margin-bottom: -180px sm:-220px (overlaps panels below)
```

---

## Bottom 3-Panel Grid

`grid grid-cols-1 md:grid-cols-[2fr_1fr_2fr]`, relative z-10.

### Panel 1 (bg-[#ECEDEC])
- Text: "Start your personalized path to natural balance" -- DM Sans 400, text-2xl sm:text-[28px] lg:text-[35px], leading-[1.1], letter-spacing -0.05em, max-w-[350px]
- Link: "Personal Assessment" -- underline, Inter 400, text-base lg:text-lg, letter-spacing -0.03em
- Decorative image (absolute right-0 bottom-0, h-full, mix-blend-multiply):
  ```
  https://meez.design/web/media/ext/c79bc389cb0bf9d4.png
  ```

### Panel 2 (bg-[#FEFDF9]) -- Auto-rotating card carousel
4 cards cycling every 3500ms with fade/slide transition:
1. FlaskConical icon, bg-black circle: "Experience our newly enhanced natural formula"
2. Leaf icon, bg-emerald-800 circle: "Pure organic ingredients sourced sustainably"
3. Droplets icon, bg-cyan-800 circle: "Advanced bioavailability for maximum absorption"
4. Sun icon, bg-amber-700 circle: "Clinically tested for daily energy & vitality"

Each card: icon in a 40px (sm:48px) round colored circle + text (Inter 400, text-sm sm:text-base lg:text-lg, text-black/80, line-height 1.2, letter-spacing -0.03em).

Active card: opacity-100 translate-y-0. Inactive: opacity-0 translate-y-4 absolute.

Bottom dots: 4 thin bars (h-0.5, flex-1, rounded-full). Active: bg-black. Inactive: bg-black/20.

### Panel 3 (bg-black)
- Left: Product image (w-[120px] h-[82px] sm:w-[160px] h-[110px] lg:w-[208px] h-[142px]):
  ```
  https://meez.design/web/media/ext/300c2e1eb0264eef.png
  ```
- Right: "+14K" (white, Inter 400, text-2xl sm:text-3xl lg:text-[35px], letter-spacing -0.05em) + "People have already optimized their wellness" (text-white/60, Inter 400, text-sm sm:text-base lg:text-lg, line-height 1.2)

---

## Desktop Floating Product (lg+ only)

Same image as mobile product, but absolutely positioned for desktop:
```
https://meez.design/web/media/ext/8f861b7c00ec34fe.png
position: absolute; z-0; hidden lg:block;
width: clamp(600px, 80vw, 1412px); height: auto;
bottom: -10%; right: clamp(-400px, -20vw, -100px);
```

---

## Animations (CSS keyframes)

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
@keyframes slideInLeft {
  from { opacity: 0; transform: translateX(-40px); }
  to { opacity: 1; transform: translateX(0); }
}
@keyframes slideInRight {
  from { opacity: 0; transform: translateX(40px); }
  to { opacity: 1; transform: translateX(0); }
}
@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.9); }
  to { opacity: 1; transform: scale(1); }
}
@keyframes wordReveal {
  from { opacity: 0; transform: translateY(100%); filter: blur(4px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0px); }
}
```

All use `cubic-bezier(0.16, 1, 0.3, 1)` easing with `both` fill mode.

**Classes and their animations:**
- `.animate-fade-up` -- fadeUp 0.8s
- `.animate-fade-in` -- fadeIn 0.7s
- `.animate-slide-left` -- slideInLeft 0.8s
- `.animate-slide-right` -- slideInRight 0.8s
- `.animate-scale-in` -- scaleIn 1s
- `.animate-word-reveal > span` -- wordReveal 0.7s

**Delay classes:** .delay-200 through .delay-1100 (increments of 0.1s)

**Animation assignments:**
- Navbar container: animate-fade-in
- Brand name: animate-slide-left delay-200
- Nav links: animate-fade-in delay-400
- Right icons: animate-slide-right delay-300
- CTA row: animate-fade-up delay-600
- Desktop product image: animate-scale-in delay-700
- Mobile product image: animate-scale-in delay-800
- Panel 1: animate-fade-up delay-900
- Panel 2: animate-fade-up delay-1000
- Panel 3: animate-fade-up delay-1100
- Inline capsule image: animate-scale-in delay-1000

### Source Code
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TerraElix</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500&family=Inter:wght@400;500&display=swap" rel="stylesheet" />
  <style>
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    @keyframes slideInLeft {
      from { opacity: 0; transform: translateX(-40px); }
      to { opacity: 1; transform: translateX(0); }
    }
    @keyframes slideInRight {
      from { opacity: 0; transform: translateX(40px); }
      to { opacity: 1; transform: translateX(0); }
    }
    @keyframes scaleIn {
      from { opacity: 0; transform: scale(0.9); }
      to { opacity: 1; transform: scale(1); }
    }
    @keyframes wordReveal {
      from { opacity: 0; transform: translateY(100%); filter: blur(4px); }
      to { opacity: 1; transform: translateY(0); filter: blur(0px); }
    }
    .animate-fade-up { animation: fadeUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) both; }
    .animate-fade-in { animation: fadeIn 0.7s cubic-bezier(0.16, 1, 0.3, 1) both; }
    .animate-slide-left { animation: slideInLeft 0.8s cubic-bezier(0.16, 1, 0.3, 1) both; }
    .animate-slide-right { animation: slideInRight 0.8s cubic-bezier(0.16, 1, 0.3, 1) both; }
    .animate-scale-in { animation: scaleIn 1s cubic-bezier(0.16, 1, 0.3, 1) both; }
    .animate-word-reveal { display: inline-block; overflow: hidden; }
    .animate-word-reveal > span { display: inline-block; animation: wordReveal 0.7s cubic-bezier(0.16, 1, 0.3, 1) both; }
    .delay-200 { animation-delay: 0.2s; }
    .delay-300 { animation-delay: 0.3s; }
    .delay-400 { animation-delay: 0.4s; }
    .delay-600 { animation-delay: 0.6s; }
    .delay-700 { animation-delay: 0.7s; }
    .delay-800 { animation-delay: 0.8s; }
    .delay-900 { animation-delay: 0.9s; }
    .delay-1000 { animation-delay: 1.0s; }
    .delay-1100 { animation-delay: 1.1s; }
  </style>
</head>
<body class="m-0 p-0">
  <div
    class="min-h-screen font-sans flex flex-col relative overflow-hidden"
    style="background-image: url('https://meez.design/web/media/ext/4dfc1a4b05bd693d.webp'); background-size: cover; background-position: center; background-repeat: no-repeat;"
  >
    <!-- Navbar -->
    <nav class="flex items-center justify-between px-5 sm:px-8 lg:px-10 py-4 lg:py-5 relative z-20 animate-fade-in">
      <span class="text-white animate-slide-left delay-200" style="font-family: 'DM Sans', sans-serif; font-size: 30px; line-height: 38px; letter-spacing: -0.05em; font-weight: 500;">TerraElix</span>

      <!-- Desktop nav -->
      <ul class="hidden md:flex gap-6 lg:gap-10 text-white/90 animate-fade-in delay-400 list-none m-0 p-0" style="font-family: 'DM Sans', sans-serif; font-size: 18px; line-height: 120%; letter-spacing: -0.01em; font-weight: 500;">
        <li class="cursor-pointer hover:text-white transition-colors">About</li>
        <li class="cursor-pointer hover:text-white transition-colors">Products</li>
        <li class="cursor-pointer hover:text-white transition-colors">Promotions</li>
        <li class="cursor-pointer hover:text-white transition-colors">Contact</li>
      </ul>

      <div class="flex items-center gap-3 lg:gap-4 animate-slide-right delay-300">
        <button class="text-white/80 hover:text-white transition-colors bg-transparent border-none cursor-pointer">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
        </button>
        <button class="text-white/80 hover:text-white transition-colors bg-transparent border-none cursor-pointer">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
        </button>
        <button class="text-white/80 hover:text-white transition-colors bg-transparent border-none cursor-pointer">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 14 4 9 9 4"/><path d="M20 20v-7a4 4 0 0 0-4-4H4"/></svg>
        </button>
        <img src="https://meez.design/web/media/ext/933e27c46b639e84.png" class="w-8 h-8 lg:w-10 lg:h-10 rounded-full object-cover" alt="Avatar" />

        <!-- Mobile menu button -->
        <button id="menuBtn" class="md:hidden text-white/80 hover:text-white transition-colors ml-2 bg-transparent border-none cursor-pointer">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="4" x2="20" y1="12" y2="12"/><line x1="4" x2="20" y1="6" y2="6"/><line x1="4" x2="20" y1="18" y2="18"/></svg>
        </button>
      </div>
    </nav>

    <!-- Mobile menu overlay -->
    <div id="mobileMenu" class="fixed inset-0 bg-black/90 z-30 flex-col items-center justify-center gap-8 md:hidden" style="display: none;">
      <button id="closeMenuBtn" class="absolute top-5 right-5 text-white bg-transparent border-none cursor-pointer">
        <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 6 6 18"/><path d="m6 6 12 12"/></svg>
      </button>
      <ul class="flex flex-col gap-6 text-white text-2xl font-medium text-center list-none m-0 p-0">
        <li class="cursor-pointer hover:text-white/70 transition-colors">About</li>
        <li class="cursor-pointer hover:text-white/70 transition-colors">Products</li>
        <li class="cursor-pointer hover:text-white/70 transition-colors">Promotions</li>
        <li class="cursor-pointer hover:text-white/70 transition-colors">Contact</li>
      </ul>
    </div>

    <!-- Hero -->
    <section class="px-5 sm:px-8 lg:px-10 flex-1 relative overflow-visible z-10 flex flex-col justify-center">
      <h1
        class="text-[48px] leading-[50px] sm:text-[80px] sm:leading-[72px] md:text-[110px] md:leading-[95px] lg:text-[130px] lg:leading-[110px] xl:text-[155px] xl:leading-[125px] m-0"
        style="font-family: 'DM Sans', sans-serif; font-weight: 400; letter-spacing: -0.05em;"
      >
        <span class="animate-word-reveal"><span class="text-white" style="animation-delay: 0.3s;">The</span></span>
        <span class="animate-word-reveal"><span class="text-white" style="animation-delay: 0.4s;">Power</span></span>
        <span class="animate-word-reveal"><span class="text-white/45" style="animation-delay: 0.5s;">of</span></span>
        <br />
        <span class="animate-word-reveal"><span class="text-white/45" style="animation-delay: 0.6s;">Nature</span></span>
        <span class="animate-word-reveal"><span class="text-white/45" style="animation-delay: 0.7s;">in</span></span>
        <span class="animate-word-reveal"><span class="text-white" style="animation-delay: 0.8s;">Every</span></span>
        <br />
        <span class="animate-word-reveal"><span class="text-white" style="animation-delay: 0.9s;">Capsule</span></span>
        <img
          src="https://meez.design/web/media/ext/014f4c2bed24ce90.png"
          alt=""
          class="hidden sm:inline-block align-middle ml-2 lg:ml-4 animate-scale-in delay-1000"
          style="height: clamp(60px, 10vw, 160px); width: auto;"
        />
      </h1>

      <div class="flex flex-col sm:flex-row sm:items-center mt-8 sm:mt-12 lg:mt-[75px] gap-5 sm:gap-8 lg:gap-[50px] animate-fade-up delay-600">
        <button
          class="flex items-center justify-center gap-2 sm:gap-3 bg-black text-white rounded-md hover:bg-neutral-900 transition-colors flex-shrink-0 w-full sm:w-[240px] md:w-[280px] lg:w-[310px] h-14 sm:h-16 lg:h-[72px] text-base sm:text-lg md:text-xl lg:text-2xl border-none cursor-pointer"
          style="font-family: 'Inter', sans-serif; font-weight: 500; letter-spacing: -0.03em;"
        >
          Explore Now
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M7 7h10v10"/><path d="M7 17 17 7"/></svg>
        </button>
        <p
          class="text-white max-w-[310px] text-sm sm:text-base lg:text-lg m-0"
          style="font-family: 'Inter', sans-serif; font-weight: 400; line-height: 1.45; letter-spacing: -0.03em;"
        >
          Discover our new plant-based supplements for daily balance and clean energy.
        </p>
      </div>
    </section>

    <!-- Mobile/Tablet product image -->
    <div class="relative z-10 flex items-center justify-center pt-0 sm:pt-2 pb-0 sm:block lg:hidden overflow-visible mb-[-180px] sm:mb-[-220px] animate-scale-in delay-800">
      <img
        src="https://meez.design/web/media/ext/8f861b7c00ec34fe.png"
        alt="Product capsules"
        class="w-[180%] sm:w-[151%] max-w-[1296px] h-auto object-contain mx-auto drop-shadow-2xl"
      />
    </div>

    <!-- Bottom panels -->
    <div class="grid grid-cols-1 md:grid-cols-[2fr_1fr_2fr] relative z-10">
      <!-- Panel 1 -->
      <div class="bg-[#ECEDEC] px-5 sm:px-8 py-6 sm:py-8 flex flex-col justify-between relative overflow-hidden min-h-[180px] sm:min-h-[200px] animate-fade-up delay-900">
        <p
          class="relative z-10 text-black max-w-[350px] text-2xl sm:text-[28px] lg:text-[35px] leading-[1.1] m-0"
          style="font-family: 'DM Sans', sans-serif; font-weight: 400; letter-spacing: -0.05em;"
        >
          Start your personalized path to natural balance
        </p>
        <span
          class="relative z-10 text-black underline underline-offset-2 cursor-pointer hover:opacity-70 transition-opacity mt-4 text-base lg:text-lg"
          style="font-family: 'Inter', sans-serif; font-weight: 400; letter-spacing: -0.03em;"
        >
          Personal Assessment
        </span>
        <img
          src="https://meez.design/web/media/ext/c79bc389cb0bf9d4.png"
          alt=""
          class="absolute right-0 bottom-0 h-full w-auto object-contain pointer-events-none z-0"
          style="mix-blend-mode: multiply;"
        />
      </div>

      <!-- Panel 2 - Gallery -->
      <div class="bg-[#FEFDF9] px-5 sm:px-8 py-6 sm:py-8 flex flex-col justify-between min-h-[150px] sm:min-h-[180px] animate-fade-up delay-1000 overflow-hidden">
        <div class="relative flex-1" id="cardContainer">
          <!-- Cards injected by JS -->
        </div>
        <div class="flex gap-2 mt-6" id="cardDots"></div>
      </div>

      <!-- Panel 3 -->
      <div class="bg-black px-5 sm:px-8 py-6 sm:py-8 flex items-center gap-4 sm:gap-6 min-h-[150px] sm:min-h-[180px] animate-fade-up delay-1100">
        <div class="flex-shrink-0">
          <img
            src="https://meez.design/web/media/ext/300c2e1eb0264eef.png"
            alt=""
            class="object-contain w-[120px] h-[82px] sm:w-[160px] sm:h-[110px] lg:w-[208px] lg:h-[142px]"
          />
        </div>
        <div>
          <p
            class="text-white text-2xl sm:text-3xl lg:text-[35px] leading-tight m-0"
            style="font-family: 'Inter', sans-serif; font-weight: 400; letter-spacing: -0.05em;"
          >
            +14K
          </p>
          <p
            class="text-white/60 mt-1 text-sm sm:text-base lg:text-lg m-0"
            style="font-family: 'Inter', sans-serif; font-weight: 400; line-height: 1.2; letter-spacing: -0.03em;"
          >
            People have already optimized their wellness
          </p>
        </div>
      </div>
    </div>

    <!-- Background decorative image - desktop only -->
    <img
      src="https://meez.design/web/media/ext/8f861b7c00ec34fe.png"
      alt=""
      class="absolute pointer-events-none z-0 hidden lg:block animate-scale-in delay-700"
      style="width: clamp(600px, 80vw, 1412px); height: auto; bottom: -10%; right: clamp(-400px, -20vw, -100px);"
    />
  </div>

  <script>
    // Mobile menu toggle
    const menuBtn = document.getElementById('menuBtn');
    const mobileMenu = document.getElementById('mobileMenu');
    const closeMenuBtn = document.getElementById('closeMenuBtn');

    menuBtn.addEventListener('click', () => {
      mobileMenu.style.display = 'flex';
    });
    closeMenuBtn.addEventListener('click', () => {
      mobileMenu.style.display = 'none';
    });

    // Card carousel
    const cards = [
      { icon: '<svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M10 2v7.527a2 2 0 0 1-.211.896L4.72 20.55a1 1 0 0 0 .9 1.45h12.76a1 1 0 0 0 .9-1.45l-5.069-10.127A2 2 0 0 1 14 9.527V2"/><path d="M8.5 2h7"/><path d="M7 16h10"/></svg>', text: 'Experience our newly enhanced natural formula', color: 'bg-black' },
      { icon: '<svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M11 20A7 7 0 0 1 9.8 6.9C15.5 4.9 17 3.5 17 3.5s1.5 0 2.8 1.3c1 .9 1.1 2.2 1.1 2.2s-1.5 1.5-3.5 7.2A7 7 0 0 1 11 20Z"/><path d="M2 21c0-3 1.9-5.6 4.4-6.3"/><path d="M12.3 7.4C14.2 5.5 17 4.5 17 4.5"/></svg>', text: 'Pure organic ingredients sourced sustainably', color: 'bg-emerald-800' },
      { icon: '<svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M7 16.3c2.2 0 4-1.83 4-4.05 0-1.16-.57-2.26-1.71-3.19S7.29 6.75 7 5.3c-.29 1.45-1.14 2.84-2.29 3.76S3 11.1 3 12.25c0 2.22 1.8 4.05 4 4.05z"/><path d="M12.56 6.6A10.97 10.97 0 0 0 14 3.02c.5 2.5 2 4.9 4 6.5s3 3.5 3 5.5a6.98 6.98 0 0 1-11.91 4.97"/></svg>', text: 'Advanced bioavailability for maximum absorption', color: 'bg-cyan-800' },
      { icon: '<svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="4"/><path d="M12 2v2"/><path d="M12 20v2"/><path d="m4.93 4.93 1.41 1.41"/><path d="m17.66 17.66 1.41 1.41"/><path d="M2 12h2"/><path d="M20 12h2"/><path d="m6.34 17.66-1.41 1.41"/><path d="m19.07 4.93-1.41 1.41"/></svg>', text: 'Clinically tested for daily energy & vitality', color: 'bg-amber-700' },
    ];

    let activeCard = 0;
    const container = document.getElementById('cardContainer');
    const dotsContainer = document.getElementById('cardDots');

    function renderCards() {
      container.innerHTML = cards.map((card, i) => `
        <div class="flex items-start gap-4 transition-all duration-500 ease-out ${i === activeCard ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4 absolute inset-0'}">
          <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-full ${card.color} flex items-center justify-center flex-shrink-0 transition-colors duration-500 text-white">
            ${card.icon}
          </div>
          <p class="text-black/80 mt-1 text-sm sm:text-base lg:text-lg m-0" style="font-family: 'Inter', sans-serif; font-weight: 400; line-height: 1.2; letter-spacing: -0.03em;">
            ${card.text}
          </p>
        </div>
      `).join('');

      dotsContainer.innerHTML = cards.map((_, i) => `
        <button data-index="${i}" class="h-0.5 flex-1 rounded-full transition-all duration-500 border-none cursor-pointer ${i === activeCard ? 'bg-black' : 'bg-black/20 hover:bg-black/40'}"></button>
      `).join('');
    }

    dotsContainer.addEventListener('click', (e) => {
      const btn = e.target.closest('button');
      if (btn && btn.dataset.index !== undefined) {
        activeCard = parseInt(btn.dataset.index);
        renderCards();
      }
    });

    renderCards();
    setInterval(() => {
      activeCard = (activeCard + 1) % cards.length;
      renderCards();
    }, 3500);
  </script>
</body>
</html>
````
