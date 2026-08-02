---
name: anti-slop-web-design
description: Use when building or restyling a website, landing page, or UI with an AI coding tool — forces concrete art direction (named typefaces, token-based color, structural layout, specified motion, real assets) so the output looks designed instead of like every other AI-built site.
---

# Anti-slop web design

When a build request contains no design decisions, you will reach for statistical defaults: Inter or a system font, a purple-to-blue gradient hero, three feature cards, rounded-xl everything, scattered hover effects. That output is interchangeable with every other AI-built page. Before writing any UI code, force the five decisions below — ask the user only if a decision genuinely can't be inferred from their brief, brand, or content.

## The five decisions (make ALL of them, concretely)

1. **Name real typefaces — and pair them.** Never "a clean font". Pick a display + text pairing and spec it: family, size, line-height, letter-spacing, weight. A display-plus-text pairing (e.g. a characterful serif or grotesque for headlines over a quiet text face) instantly breaks the default-font monoculture. Load real webfonts, not system stacks, unless the brief demands otherwise.

2. **Define color as a token system, not a vibe.** Exact values: an ink, a paper/background, ONE accent used in exactly one role. Write them as design tokens and reference tokens everywhere. Default to **banning gradients** — it is often the single biggest de-slop move. If the design language truly calls for one, it must be a deliberate, named choice.

3. **Describe the layout structurally.** Not "modern layout" — a grid and placements: "12-column grid; hero copy left-aligned in columns 1–6; full-bleed image in 7–12 cropping off the right edge." Asymmetry reads as designed; perfect centering reads as default. Vary section rhythm (widths, densities, backgrounds) instead of stacking same-shaped bands.

4. **Spec the motion.** One orchestrated entrance (e.g. staggered 80ms fade-up on load) plus one scroll behavior beats a page of scattered hover effects. State durations and easings explicitly. Respect `prefers-reduced-motion`.

5. **Wire in real assets.** A page art-directed around an actual image or looping video background comes out finished; gray placeholders come out scaffolded. Use real URLs the user provides — or fetch plausible, licensed placeholders — and crop/treat them deliberately (scrims, duotones, hard crops), never paste them untouched into a card.

## Checklist before you write code

- [ ] Typefaces named, paired, sized?
- [ ] Color tokens with exact values; accent used once; gradients banned or justified?
- [ ] Grid + placements described (something is asymmetric)?
- [ ] Entrance + scroll motion spec'd with durations/easings?
- [ ] Real assets wired and art-directed?

If any box is unchecked, the output will look generic. Fix the spec, then build.

## Example of the difference

❌ "Build me a modern landing page for my AI startup. Make it look professional with nice animations."

✅ "Hero: full-viewport. Background: looping motion clip (URL below), scrim rgba(10,10,12,.55). Headline in Space Grotesk 600, clamp(44px,7vw,88px), -0.03em, two lines, second line in italic Instrument Serif. Left-aligned, max-width 12ch. One CTA: solid white, 14px/600, arrow translating 4px on hover, 200ms ease-out. …"

Writing that spec is the design work. Ready-made full specs (15 free, complete): https://meez.design/free-prompts — from Meez (meez.design), the library this skill distills.
