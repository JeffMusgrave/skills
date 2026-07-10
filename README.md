# Skills

[![skills.sh](https://skills.sh/b/jakubkrehel/skills)](https://skills.sh/jakubkrehel/skills)

[Agent Skills](https://docs.anthropic.com/en/docs/claude-code/skills) for design engineering — typography, interface polish and color. They teach AI coding assistants (Claude Code, Codex, Cursor and others) the details that compound into a great interface.

Each skill is distilled from my own writing and tools, so the agent applies the same decisions I would make by hand.

## Install

```bash
npx skills@latest add jakubkrehel/skills
```

Or install a single skill:

```bash
npx skills@latest add jakubkrehel/skills --skill great-typography
```

## The skills

### great-typography

How to choose and work with type on the web, from picking a typeface to the finishing details. Based on [Typography manual for the web](https://jakub.kr/writing/typography-manual-for-the-web) and [Working with type](https://jakub.kr/writing/working-with-type). It deliberately stays out of how fonts are loaded.

- Choosing and pairing typefaces, font formats (`.woff2` on the web)
- Variable fonts, axes, `font-synthesis` and OpenType features (`tnum`, `zero`, `liga`, stylistic sets)
- Type scales with semantic names; line-height, letter-spacing and text trimming with `text-box`
- Measure, wrapping (`text-wrap: balance` / `pretty`) and truncation
- Smart punctuation, internationalization, underlines, selection, placeholders and carets
- iOS input zoom workarounds, WCAG contrast, font smoothing
- A cheat sheet of every typography CSS property covered

### make-interfaces-feel-better

The small design engineering details that make interfaces feel polished. Based on [Details that make interfaces feel better](https://jakub.kr/writing/details-that-make-interfaces-feel-better).

- Text wrapping, concentric border radius, optical vs geometric alignment
- Contextual icon animations with opacity, scale and blur
- Interruptible animations, enter animations with split and stagger, subtle exits
- Font smoothing on macOS, tabular numbers for dynamic values
- Shadows instead of borders, image outlines for depth

### oklch-skill

Working with the OKLCH color space in web projects — the perceptually uniform color space that eliminates hue drift, makes palette generation predictable and simplifies accessibility fixes. Based on [oklch.fyi](https://oklch.fyi).

- Converting hex, rgb and hsl to oklch
- Generating perceptually uniform palette scales (50–950) and dark mode via lightness
- WCAG 2 and APCA contrast checking, hue drift detection in HSL-based palettes
- sRGB and Display P3 gamut boundaries with CSS fallback patterns
- Tailwind v4 oklch theming and custom tokens

## License

[MIT](./LICENSE)
