# Taste Skill (Svelte 5)

[![GitHub stars](https://img.shields.io/github/stars/WildSoul47/taste-skill-svelte?style=flat-square&color=yellow)](https://github.com/WildSoul47/taste-skill-svelte/stargazers)
[![Agent Skills](https://img.shields.io/badge/Agent_Skills-Compatible-blue?style=flat-square)](https://github.com/vercel-labs/agent-skills)
[![AI Supported](https://img.shields.io/badge/AI_Supported-Claude_%7C_Cursor_%7C_Copilot_%7C_Gemini-black?style=flat-square)](#)
[![SvelteKit](https://img.shields.io/badge/Stack-SvelteKit_%2B_Scoped_CSS-%23FF3E00?style=flat-square)](#)

> **Inspired by [taste-skill](https://github.com/Leonxlnx/taste-skill) by [Leonxlnx](https://github.com/Leonxlnx)** — a collection of skills that improve how AI tools write frontend code.

A Svelte 5 adaptation of the original taste-skill. Same design philosophy and anti-slop rules, rewritten for **SvelteKit + Scoped CSS + CSS Variables** — no Tailwind, no framer-motion, pure Svelte.

## Why This Exists

The original taste-skill is excellent but heavily coupled to React/Next.js, Tailwind CSS, and framer-motion. This project ports every skill to Svelte 5's native APIs:

| Original (React) | This Version (Svelte 5) |
|---|---|
| framer-motion | `svelte/transition` + `svelte/motion` (built-in) |
| Tailwind CSS | Scoped CSS + CSS Variables |
| `"use client"` / Client Components | Not needed — all `.svelte` files are universal |
| `useState` / `useEffect` | `$state` / `$effect` runes |
| `React.memo` | Not needed — no virtual DOM |
| `AnimatePresence` | `{#key}` blocks + `transition:` directives |
| `layoutId` | `crossfade` + `animate:flip` |
| `whileInView` | Svelte actions + `IntersectionObserver` |

## Installing

```bash
npx skills add https://github.com/WildSoul47/taste-skill-svelte
```

## Skills

| Skill | Description |
| --- | --- |
| **taste-skill** | The main design skill for premium SvelteKit frontend code. Covers layout, typography, colors, spacing, and motion — with the 3-dial config system (DESIGN_VARIANCE, MOTION_INTENSITY, VISUAL_DENSITY). |
| **redesign-skill** | For upgrading existing SvelteKit projects by auditing and fixing design problems. |
| **soft-skill** | Premium, soft UI look with expensive fonts, whitespace, depth, and smooth spring animations. |
| **output-skill** | Prevents AI from being lazy, skipping code blocks, or using placeholder comments. (Framework-agnostic — identical to original) |
| **minimalist-skill** | Clean, editorial-style interfaces (Notion/Linear style) with warm monochrome palettes and scoped CSS. |
| **brutalist-skill** | Raw mechanical interfaces, Swiss typography, extreme scale contrast. (Beta) |
| **stitch-skill** | Google Stitch-compatible semantic design rules for premium AI UI generation. |

## Settings (taste-skill only)

The taste skill has three settings at the top of the file. Change these numbers (1–10) depending on what you're building:

- **DESIGN_VARIANCE** — How experimental the layout is. (1–3: Clean/centered | 8–10: Asymmetric/modern)
- **MOTION_INTENSITY** — How much animation there is. (1–3: Simple hover | 8–10: Spring physics/scroll-triggered)
- **VISUAL_DENSITY** — How much content fits on one screen. (1–3: Spacious/luxury | 8–10: Dense dashboards)

## Differences from the Original

- **Zero Tailwind dependency** — All styling uses scoped CSS in `<style>` blocks with CSS custom properties as design tokens.
- **Zero animation library dependency** — Uses Svelte's built-in `svelte/transition`, `svelte/animate`, and `svelte/motion` (spring/tweened stores).
- **Simpler mental model** — No server/client component boundaries, no memoization concerns, no dependency arrays.
- **Smaller bundle** — Svelte compiles away; no virtual DOM runtime.

## What Was Kept Unchanged

The original taste-skill's greatest value is its **design rule system**, not the framework code. These sections are kept (nearly) verbatim:

- Typography rules (Geist, Outfit, Satoshi, tracking-tight)
- Color calibration (max 1 accent, saturation <80%, no AI purple)
- Anti-slop directives and AI Tells
- Layout diversification rules
- Performance guardrails (GPU-safe animation, z-index discipline)
- The Creative Arsenal (interaction pattern catalog)
- The output-skill in its entirety

## Feedback & Contact

- Open a Pull Request or Issue right here on GitHub
- Email: [345931036@qq.com](mailto:345931036@qq.com)

## Credits

- **Original project:** [taste-skill](https://github.com/Leonxlnx/taste-skill) by [Leonxlnx](https://github.com/Leonxlnx)
- Design philosophy, 3-dial system, anti-slop rules, and the Creative Arsenal are all from the original project.

## License

MIT
