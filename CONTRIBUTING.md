# Contributing

Prompt PRs are welcome. The bar is simple: **a submission must pass the anti-slop test** — all five decisions made concretely, no vibes.

## What a submitted prompt must contain

1. **Named typefaces** — a real display + text pairing with weights/sizes, loaded as webfonts.
2. **A token color system** — exact values for ink / paper / one accent, referenced as tokens. No unexamined gradients.
3. **Structural layout** — grid, placements, section rhythm. "Modern and clean" is an automatic decline.
4. **Specified motion** — entrance + scroll behavior with durations and easings, `prefers-reduced-motion` respected.
5. **Real assets** — working image/video URLs (licensed or placeholder services), treated deliberately.

## Format

Copy the structure of any file in [`prompts/`](prompts/): a heading, the Category/Source/License line, the one-line usage note, then the complete prompt text in a four-backtick fence. The prompt must build a working page when pasted into Lovable, Bolt, v0, Cursor or Claude Code — test it in at least one of them and say which in the PR description.

## What gets declined

- Prompts that are style-transfer of an existing site's protected assets or trade dress
- Teasers ("full version on my site") — everything merged here must be complete
- Anything whose output you didn't actually build and look at

By submitting, you license your prompt text under the same terms as the rest of the repo (free to use, including commercially).
