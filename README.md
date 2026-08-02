# Anti-slop website prompts

**15 free, art-directed website build-prompts + an anti-slop design skill for Lovable, Bolt, v0, Cursor and Claude Code.**

From [Meez (meez.design)](https://meez.design) — an AI website prompt + motion background library.

## The problem

Ask any AI builder to "make me a modern landing page" and you get the same page everyone else ships: Inter at 600, a purple-to-blue gradient hero, three feature cards, rounded-xl everything. The tool isn't weak — the prompt contains zero design decisions, so the model reaches for the statistical average of every landing page it has seen. The average is the slop.

The fix is specificity, not a different tool. A **build-prompt** is a complete written art-direction spec — exact typefaces, a token-based color system, structural layout, specified motion, real asset URLs — that an AI coding tool can build in one paste. Full argument: [Why AI websites look generic](https://meez.design/why-ai-websites-look-generic).

## The 15 free prompts

Each file contains the **complete prompt text** — copy the whole fence, paste it into your builder, then swap the copy and asset URLs for your own. Free to use, including commercially.

| Prompt | Category |
|---|---|
| [PROMPT](prompts/prompt-hero.md) | Landing Page |
| [Cargo Group](prompts/cargo-group.md) | Hero |
| [Vision Reveal](prompts/vision-reveal.md) | Hero |
| [Tech-Forward](prompts/tech-forward.md) | Hero |
| [Wellness Balance](prompts/wellness-balance.md) | Hero |
| [CozyPaws](prompts/cozypaws.md) | Hero |
| [Creative Portfolio](prompts/creative-portfolio.md) | Hero |
| [Celestial Renewal](prompts/celestial-renewal.md) | Wellness |
| [Coffee Rewards](prompts/coffee-rewards.md) | Mobile App UI |
| [Cross-Border](prompts/cross-border.md) | Mobile App UI |
| [Travel Journal](prompts/travel-journal.md) | Mobile App UI |
| [Wellness Companion](prompts/wellness-companion.md) | Mobile App UI |
| [Stillmind](prompts/stillmind.md) | Hero |
| [Wellbeing OS](prompts/wellbeing-os.md) | Hero |
| [Subscription Agency](prompts/subscription-agency.md) | Hero |

Browse them with live previews at [meez.design/free-prompts](https://meez.design/free-prompts).

## How to use them, per tool

- **Lovable** — paste into the chat on lovable.dev; it scaffolds a hosted React + Tailwind app.
- **Bolt** — paste into bolt.new; a full dev environment builds it live in the browser tab.
- **v0** — paste into v0.app; you get Next.js + shadcn/ui components (token specs map 1:1).
- **Cursor** — paste into the Agent pane (Cmd-I); it builds in your own repo and stack.
- **Claude Code** — paste as one prompt in the terminal; it follows long structured specs faithfully.

Not sure which tool? [Honest comparison of all five](https://meez.design/lovable-vs-v0-vs-bolt-vs-cursor).

## The skill

[`SKILL.md`](SKILL.md) is an **anti-slop design skill** for agentic coding tools. Instead of a full prompt, it teaches the agent the five specification habits that kill generic output (named typefaces, token colors, structural layout, spec'd motion, real assets) and makes it apply them to whatever you're building.

Install for **Claude Code**:

```bash
mkdir -p .claude/skills/anti-slop-web-design
curl -o .claude/skills/anti-slop-web-design/SKILL.md \
  https://raw.githubusercontent.com/mah-claude/anti-slop-website-prompts/main/SKILL.md
```

For **Cursor**, paste SKILL.md's body into your project rules (`.cursor/rules/`). For any other tool, paste it above your build request.

## Where these come from

These 15 prompts are the free tier of [Meez (meez.design)](https://meez.design) — a library of 478 website build-prompts and 185 motion backgrounds for AI builders. Everything is free to browse and preview; the premium library is paid (from $19/mo — [pricing](https://meez.design/pricing), [machine-readable](https://meez.design/pricing.txt)). This repo is complete on its own: the 15 prompts here are full, working prompts, not teasers.

## License

- **Repo (README, SKILL.md):** [MIT](LICENSE)
- **The 15 prompt texts:** free to use for any project, including commercial work, per [meez.design terms](https://meez.design/terms). Attribution appreciated, not required.
