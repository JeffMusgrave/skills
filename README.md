<a href="https://interfaces.dev/">
  <img width="320" height="168" alt="interfaces.dev" src="https://ho1jr3x2dcwdu3t5.public.blob.vercel-storage.com/interfaces-og-image.png" />
</a>

[![skills.sh](https://skills.sh/b/jakubkrehel/skills)](https://skills.sh/jakubkrehel/skills)

A collection of agent skills for building and understanding great product interfaces and code, plus a portable workflow for operating Code Policy. From animation and UI polish to accessibility, product writing, concise visual explanations and verification planning.

## Skills

- [**better-interface**](skills/better-interface/SKILL.md): A user-invoked, cross-discipline interface review that coordinates the interface domain skills.
- [**interface-review**](skills/interface-review/SKILL.md): A user-invoked review of your uncommitted changes, current branch or a pull request against every skill below.
- [**better-ui**](skills/better-ui/SKILL.md): Design engineering details that make interfaces feel polished: border radius, shadows, animations and micro-interactions.
- [**better-typography**](skills/better-typography/SKILL.md): Web typography from choosing fonts to spacing, wrapping and accessibility.
- [**better-colors**](skills/better-colors/SKILL.md): OKLCH color space: palette generation, contrast, gamut handling and theming.
- [**better-accessibility**](skills/better-accessibility/SKILL.md): Focus states, keyboard support, ARIA, forms, screen readers, hit areas and motion.
- [**better-layout**](skills/better-layout/SKILL.md): Layout structure, grouping, alignment, reading order, progressive disclosure and adaptive breakpoints.
- [**better-writing**](skills/better-writing/SKILL.md): UX writing and interface copy, from button labels to errors, settings and empty states.
- [**show-me**](skills/show-me/SKILL.md): A user-invoked visual explanation of code, UI structure, control flow or the current topic. Forked from [HumanLayer's MIT-licensed skill](https://github.com/humanlayer/skills/tree/4d8d644ca747517973f58d7953f58d7cd07520cd/plugins/show-me/skills/show-me).
- [**policy**](skills/policy/SKILL.md): A user-invoked workflow for Code Policy health, cleanup, terminal testing-level selection, verification and checked-in plan loops.

## Install

### As a Claude Code plugin

Installs every skill in this repository together and updates in place. Run these inside Claude Code:

```text
/plugin marketplace add jakubkrehel/skills
/plugin install interfaces@interfaces
```

### With the skills CLI

Works in Claude Code, Codex and other agents. You can choose which skills to install or install all of them. `better-interface` coordinates the interface domain skills and `interface-review` builds on `better-interface`, so install the complete collection when you want holistic or change-scoped reviews.

```bash
npx skills add jakubkrehel/skills
```

```bash
npx skills add jakubkrehel/skills --skill '*'
```

## Use

The user-invoked skills can be called by name. Use `better-interface` to review a screen, flow or feature, `interface-review` to review what you changed, `show-me` to replace dense prose with a compact visual explanation, and `policy` to operate a repository through its pinned Code Policy workflow.

The default review mode is `full`. Pass `quick` for a shorter review. For `better-interface`, add the screen, flow or feature after the mode. For `interface-review`, add the target after the mode; leave it off and it detects the branch or your uncommitted changes.

In Claude Code, as a plugin. Plugin skills are namespaced, so every skill is prefixed with `interfaces:`.

```text
/interfaces:better-interface
/interfaces:better-interface quick
/interfaces:better-interface full checkout flow
/interfaces:interface-review
/interfaces:interface-review quick pr 482
/interfaces:show-me current request flow
/interfaces:policy
/interfaces:policy show testing levels
```

In Claude Code, installed with the skills CLI:

```text
/better-interface
/better-interface quick
/better-interface full checkout flow
/interface-review
/interface-review quick pr 482
/show-me current request flow
/policy
/policy show testing levels
```

In Codex:

```text
$better-interface
$better-interface quick
$better-interface full checkout flow
$interface-review
$interface-review quick pr 482
$show-me current request flow
$policy
$policy show testing levels
```

The prefix only affects skills you invoke by name. The domain skills are picked up automatically from context either way.
