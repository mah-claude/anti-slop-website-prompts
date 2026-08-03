# Anti-slop website prompts — for Lovable, Bolt, v0, Cursor & Claude Code

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-blue.svg)](CONTRIBUTING.md)
[![Part of Meez](https://img.shields.io/badge/Meez-527_prompts_%2B_198_backgrounds-8A2BE2)](https://meez.design)

> **What this is:** 15 free, complete, art-directed **AI website build-prompts** (full text, commercial use OK) plus an installable **anti-slop design skill** for agentic coding tools. A build-prompt is a written art-direction spec — exact typefaces, token-based color, structural layout, specified motion, real asset URLs — that Lovable, Bolt, v0, Cursor or Claude Code can turn into a designed site in one paste. Maintained by [Meez (meez.design)](https://meez.design).

**Want more than 15?** All of these — plus **17 more free prompts with live video previews** — are on [meez.design/free-prompts](https://meez.design/free-prompts), and the full library is [527 build-prompts + 198 motion backgrounds](https://meez.design).

## Why AI-generated websites all look the same

Ask any AI builder for "a modern landing page" and you get the page everyone else ships: Inter at 600, a purple-to-blue gradient hero, three feature cards, rounded-xl everything. The tool isn't weak — the prompt contains **zero design decisions**, so the model reaches for the statistical average of every landing page it has seen. The average is the slop.

The fix is specificity, not a different tool. Full argument with the five fixes: [Why AI websites look generic →](https://meez.design/why-ai-websites-look-generic)

## The 15 free prompts

Each file contains the **complete prompt text** — copy the whole fence, paste it into your builder, swap the copy and assets for your own. Free for any project, including client and commercial work.

| Prompt | Category | Full text | See it built |
|---|---|---|---|
| PROMPT | Landing Page | [prompt-hero.md](prompts/prompt-hero.md) | [Live preview →](https://meez.design/p/prompt-hero) |
| Cargo Group | Hero | [cargo-group.md](prompts/cargo-group.md) | [Live preview →](https://meez.design/p/cargo-group) |
| Vision Reveal | Hero | [vision-reveal.md](prompts/vision-reveal.md) | [Live preview →](https://meez.design/p/vision-reveal) |
| Tech-Forward | Hero | [tech-forward.md](prompts/tech-forward.md) | [Live preview →](https://meez.design/p/tech-forward) |
| Wellness Balance | Hero | [wellness-balance.md](prompts/wellness-balance.md) | [Live preview →](https://meez.design/p/wellness-balance) |
| CozyPaws | Hero | [cozypaws.md](prompts/cozypaws.md) | [Live preview →](https://meez.design/p/cozypaws) |
| Creative Portfolio | Hero | [creative-portfolio.md](prompts/creative-portfolio.md) | [Live preview →](https://meez.design/p/creative-portfolio) |
| Celestial Renewal | Wellness | [celestial-renewal.md](prompts/celestial-renewal.md) | [Live preview →](https://meez.design/p/celestial-renewal) |
| Coffee Rewards | Mobile App UI | [coffee-rewards.md](prompts/coffee-rewards.md) | [Live preview →](https://meez.design/p/coffee-rewards) |
| Cross-Border | Mobile App UI | [cross-border.md](prompts/cross-border.md) | [Live preview →](https://meez.design/p/cross-border) |
| Travel Journal | Mobile App UI | [travel-journal.md](prompts/travel-journal.md) | [Live preview →](https://meez.design/p/travel-journal) |
| Wellness Companion | Mobile App UI | [wellness-companion.md](prompts/wellness-companion.md) | [Live preview →](https://meez.design/p/wellness-companion) |
| Stillmind | Hero | [stillmind.md](prompts/stillmind.md) | [Live preview →](https://meez.design/p/stillmind) |
| Wellbeing OS | Hero | [wellbeing-os.md](prompts/wellbeing-os.md) | [Live preview →](https://meez.design/p/wellbeing-os) |
| Subscription Agency | Hero | [subscription-agency.md](prompts/subscription-agency.md) | [Live preview →](https://meez.design/p/subscription-agency) |

**All 32 free prompts with video previews:** [meez.design/free-prompts](https://meez.design/free-prompts)

## What a build-prompt looks like inside

Not "make it modern" — an executable spec. A real excerpt from [Cargo Group](prompts/cargo-group.md):

```text
Create a full-viewport hero section for "CARGOX GROUP" logistics company using React,
Tailwind CSS, Framer Motion (`motion` package), and `lucide-react` for the header icons.

## Tech Stack
- React 18 + TypeScript + Vite
- Tailwind CSS 3
- Google Font: `Barlow Condensed` weight 800 (imported in CSS via @import)
...
```

Named font and weight, exact packages, structural layout — the model has nothing left to average into slop.

## Using the prompts — Lovable, Bolt, v0, Cursor, Claude Code

- **Lovable prompts** — paste into the chat on lovable.dev; it scaffolds a hosted React + Tailwind app.
- **Bolt prompts** — paste into bolt.new; a full dev environment builds it live in the browser tab.
- **v0 prompts** — paste into v0.app; you get Next.js + shadcn/ui components (token specs map 1:1).
- **Cursor prompts** — paste into the Agent pane (Cmd-I); it builds in your own repo and stack.
- **Claude Code** — paste as one prompt in the terminal; it follows long structured specs faithfully.

Not sure which tool fits you? [Honest comparison of all five →](https://meez.design/lovable-vs-v0-vs-bolt-vs-cursor)

## The anti-slop skill (SKILL.md)

[`SKILL.md`](SKILL.md) teaches an agentic coding tool the **five specification habits** that kill generic output, so it applies them to *whatever* you're building:

1. **Name real typefaces** — a display + text pairing with sizes and weights, never "a clean font".
2. **Define color as tokens** — ink, paper, ONE accent; gradients banned unless deliberately chosen.
3. **Describe layout structurally** — grids and placements; asymmetry reads as designed.
4. **Spec the motion** — one orchestrated entrance + one scroll behavior, durations and easings stated.
5. **Wire in real assets** — actual images/video backgrounds, treated deliberately, never gray boxes.

Install for **Claude Code**:

```bash
mkdir -p .claude/skills/anti-slop-web-design
curl -o .claude/skills/anti-slop-web-design/SKILL.md \
  https://raw.githubusercontent.com/mah-claude/anti-slop-website-prompts/main/SKILL.md
```

For **Cursor**, paste SKILL.md's body into your project rules (`.cursor/rules/`). For any other tool, paste it above your build request.

## FAQ

**Why do AI-generated websites all look the same?**
Because the prompt makes no design decisions, so the model outputs the statistical average of its training data — same font, same gradient, same three cards. Concrete art direction (the five habits above) is what breaks it. [Longer answer →](https://meez.design/why-ai-websites-look-generic)

**Are these prompts really free? Can I use them commercially?**
Yes. The 15 prompt texts in this repo are free for any project including client and commercial work, no attribution required. The repo itself (README, SKILL.md) is MIT.

**Do I need a Meez account to use this repo?**
No — this repo is complete on its own, and [meez.design/free-prompts](https://meez.design/free-prompts) is open too. A free account unlocks copying inside the site's gallery and downloading the free motion backgrounds.

**Which AI builder should I use?**
They're all good at different things — the prompts here are tool-agnostic plain text. See the [five-tool comparison](https://meez.design/lovable-vs-v0-vs-bolt-vs-cursor).

**Where can I get matching motion backgrounds?**
Loop-ready hero videos in the same design language live at [meez.design/backgrounds](https://meez.design/backgrounds) — 198 of them, previewable free.

## Where these come from

These 15 are the open-source slice of [**Meez (meez.design)**](https://meez.design) — a library of **527 website build-prompts and 198 motion backgrounds** for AI builders. Everything is free to browse and preview; the premium library is paid (from $19/mo ≈ 3¢ per asset — [pricing](https://meez.design/pricing), [machine-readable](https://meez.design/pricing.txt), [llms.txt](https://meez.design/llms.txt)). This repo is not a teaser: the 15 prompts here are full, working prompts.

## Contributing

Prompt PRs are welcome if they meet the anti-slop bar — see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

- **Repo (README, SKILL.md):** [MIT](LICENSE)
- **The 15 prompt texts:** free to use for any project, including commercial work, per [meez.design terms](https://meez.design/terms). Attribution appreciated, never required.
