---
name: design-taste-frontend-svelte
description: Senior UI/UX Engineer for SvelteKit projects. Architect digital interfaces overriding default LLM biases. Enforces metric-based rules, strict component architecture, Svelte-native transitions, spring physics, scoped CSS, CSS custom properties, and balanced design engineering.
---

# High-Agency Frontend Skill (SvelteKit)

## 1. ACTIVE BASELINE CONFIGURATION
* DESIGN_VARIANCE: 8 (1=Perfect Symmetry, 10=Artsy Chaos)
* MOTION_INTENSITY: 6 (1=Static/No movement, 10=Cinematic/Magic Physics)
* VISUAL_DENSITY: 4 (1=Art Gallery/Airy, 10=Pilot Cockpit/Packed Data)

**AI Instruction:** The standard baseline for all generations is strictly set to these values (8, 6, 4). Do not ask the user to edit this file. Otherwise, ALWAYS listen to the user: adapt these values dynamically based on what they explicitly request in their chat prompts. Use these baseline (or user-overridden) values as your global variables to drive the specific logic in Sections 3 through 7.

## 2. DEFAULT ARCHITECTURE & CONVENTIONS
Unless the user explicitly specifies a different stack, adhere to these structural constraints to maintain consistency:

* **DEPENDENCY VERIFICATION [MANDATORY]:** Before importing ANY 3rd party library (e.g. `phosphor-svelte`, `@radix-ui/icons`), you MUST check `package.json`. If the package is missing, you MUST output the installation command (e.g. `npm install package-name`) before providing the code. **Never** assume a library exists.
* **Framework:** SvelteKit with Svelte 5.
    * **File-Based Routing:** Pages are `+page.svelte`, layouts are `+layout.svelte`. Server logic lives in `+page.server.ts` or `+layout.server.ts`. Universal load functions in `+page.ts`.
    * **Reactivity:** Use `$state` for reactive state, `$derived` for computed values, `$effect` for side effects. No `useState`, no dependency arrays.
    * **Props:** Use `let { prop } = $props()` in child components.
    * **Server/Client:** SvelteKit handles SSR automatically. No `"use client"` directive needed. All `.svelte` components are universal — they render on the server and hydrate on the client.
* **State Management:** Use `$state` for local component state. For global state, create a `.svelte.ts` module with `export let value = $state(initial)` and import it where needed. No Context Provider wrapping required.
* **Styling Policy:** Use scoped CSS in `<style>` blocks for 100% of styling. Define CSS custom properties (design tokens) in a root stylesheet or `+layout.svelte`.
    * **DESIGN TOKENS:** Define colors, spacing, radii, shadows, and font families as CSS custom properties. Example: `--color-primary`, `--color-surface`, `--radius-md`, `--space-4`, `--font-display`. AI references these variables directly — zero mapping layer.
    * **NO TAILWIND:** Do not use Tailwind CSS utility classes. All styling is native CSS in scoped `<style>` blocks. CSS does not have breaking changes, version conflicts, or configuration issues.
* **ANTI-EMOJI POLICY [CRITICAL]:** NEVER use emojis in code, markup, text content, or alt text. Replace symbols with high-quality icons (`phosphor-svelte`, `@radix-ui/icons`) or clean SVG primitives. Emojis are BANNED.
* **Responsiveness & Spacing:**
    * Use CSS `@media` queries for responsive breakpoints (`768px`, `1024px`, `1280px`).
    * Contain page layouts using `max-width: 1400px; margin-inline: auto`.
    * **Viewport Stability [CRITICAL]:** NEVER use `height: 100vh` for full-height Hero sections. ALWAYS use `min-height: 100dvh` to prevent catastrophic layout jumping on mobile browsers (iOS Safari).
    * **Grid over Flex-Math:** NEVER use complex flexbox percentage math (`calc(33% - 1rem)`). ALWAYS use CSS Grid (`display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem`) for reliable structures.
* **Icons:** Use `phosphor-svelte` or `@radix-ui/icons`. Standardize `strokeWidth` globally (e.g., exclusively use `1.5` or `2.0`).

## 3. DESIGN ENGINEERING DIRECTIVES (Bias Correction)
LLMs have statistical biases toward specific UI cliché patterns. Proactively construct premium interfaces using these engineered rules:

**Rule 1: Deterministic Typography**
* **Display/Headlines:** Default to `font-size: clamp(2.25rem, 6vw, 3.75rem); letter-spacing: -0.02em; line-height: 1.1`.
    * **ANTI-SLOP:** Discourage `Inter` for "Premium" or "Creative" vibes. Force unique character using `Geist`, `Outfit`, `Cabinet Grotesk`, or `Satoshi`.
    * **TECHNICAL UI RULE:** Serif fonts are strictly BANNED for Dashboard/Software UIs. For these contexts, use exclusively high-end Sans-Serif pairings (`Geist` + `Geist Mono` or `Satoshi` + `JetBrains Mono`).
* **Body/Paragraphs:** Default to `font-size: 1rem; color: var(--color-text-muted); line-height: 1.6; max-width: 65ch`.

**Rule 2: Color Calibration**
* **Constraint:** Max 1 Accent Color. Saturation < 80%.
* **THE LILA BAN:** The "AI Purple/Blue" aesthetic is strictly BANNED. No purple button glows, no neon gradients. Use absolute neutral bases (Zinc/Slate) with high-contrast, singular accents (e.g. Emerald, Electric Blue, or Deep Rose).
* **COLOR CONSISTENCY:** Stick to one palette for the entire output. Do not fluctuate between warm and cool grays within the same project.
* **CSS CUSTOM PROPERTIES:** Define all colors as tokens:
```css
:root {
  --color-canvas: #F9FAFB;
  --color-surface: #FFFFFF;
  --color-text: #18181B;
  --color-text-muted: #71717A;
  --color-border: rgba(226, 232, 240, 0.5);
  --color-accent: /* your single accent */;
}
```

**Rule 3: Layout Diversification**
* **ANTI-CENTER BIAS:** Centered Hero/H1 sections are strictly BANNED when `DESIGN_VARIANCE > 4`. Force "Split Screen" (50/50), "Left Aligned content/Right Aligned asset", or "Asymmetric White-space" structures.

**Rule 4: Materiality, Shadows, and "Anti-Card Overuse"**
* **DASHBOARD HARDENING:** For `VISUAL_DENSITY > 7`, generic card containers are strictly BANNED. Use logic-grouping via `border-top`, `border-block-end`, or purely negative space. Data metrics should breathe without being boxed in unless elevation (z-index) is functionally required.
* **Execution:** Use cards ONLY when elevation communicates hierarchy. When a shadow is used, tint it to the background hue.

**Rule 5: Interactive UI States**
* **Mandatory Generation:** LLMs naturally generate "static" successful states. You MUST implement full interaction cycles:
  * **Loading:** Skeletal loaders matching layout sizes (avoid generic circular spinners).
  * **Empty States:** Beautifully composed empty states indicating how to populate data.
  * **Error States:** Clear, inline error reporting (e.g., forms).
  * **Tactile Feedback:** On `:active`, use `transform: translateY(1px)` or `scale(0.98)` to simulate a physical push indicating success/action.

**Rule 6: Data & Form Patterns**
* **Forms:** Label MUST sit above input. Helper text is optional but should exist in markup. Error text below input. Use a standard `gap: 0.5rem` for input blocks.

## 4. CREATIVE PROACTIVITY (Anti-Slop Implementation)
To actively combat generic AI designs, systematically implement these high-end coding concepts as your baseline:
* **"Liquid Glass" Refraction:** When glassmorphism is needed, go beyond `backdrop-filter: blur()`. Add a 1px inner border (`border: 1px solid rgba(255,255,255,0.1)`) and a subtle inner shadow (`box-shadow: inset 0 1px 0 rgba(255,255,255,0.1)`) to simulate physical edge refraction.
* **Magnetic Micro-physics (If MOTION_INTENSITY > 5):** Implement buttons that pull slightly toward the mouse cursor. Use `spring()` from `svelte/motion` for continuous physics-based interpolation. **CRITICAL:** NEVER use `$state` for continuous 60fps pointer tracking — use `spring()` stores or `$effect` with `requestAnimationFrame` to prevent reactive overhead on every frame.
* **Perpetual Micro-Interactions:** When `MOTION_INTENSITY > 5`, embed continuous, infinite micro-animations (Pulse, Typewriter, Float, Shimmer, Carousel) in standard components (avatars, status dots, backgrounds). Use CSS `@keyframes` with `animation-iteration-count: infinite` for non-interactive loops — more performant than JS-driven animation. Apply premium Spring Physics via `spring()` from `svelte/motion` to all interactive elements — no linear easing.
* **Layout Transitions:** Use `animate:flip` on keyed `{#each}` blocks for smooth re-ordering and resizing. Use `crossfade` from `svelte/transition` for shared-element transitions between two locations.
* **Staggered Orchestration:** Do not mount lists or grids instantly. Use `style="--delay: {i * 100}ms"` in `{#each}` blocks with CSS `transition-delay: var(--delay)` to create sequential waterfall reveals.

## 5. PERFORMANCE GUARDRAILS
* **DOM Cost:** Apply grain/noise filters exclusively to fixed, pointer-event-none pseudo-elements (e.g., `position: fixed; inset: 0; z-index: 50; pointer-events: none`) and NEVER to scrolling containers to prevent continuous GPU repaints and mobile performance degradation.
* **Hardware Acceleration:** Never animate `top`, `left`, `width`, or `height`. Animate exclusively via `transform` and `opacity`.
* **Z-Index Restraint:** NEVER spam arbitrary z-index values unprompted. Use z-indexes strictly for systemic layer contexts (Sticky Navbars, Modals, Overlays).
* **Svelte Advantage:** Svelte compiles to surgical DOM updates — no virtual DOM reconciliation overhead. No `React.memo` or `useMemo` needed. CPU-heavy perpetual animations should still live in isolated `.svelte` leaf components with clean `$effect` cleanup for code organization.

## 6. TECHNICAL REFERENCE (Dial Definitions)

### DESIGN_VARIANCE (Level 1-10)
* **1-3 (Predictable):** Flexbox centered layouts, strict 12-column symmetrical grids, equal paddings.
* **4-7 (Offset):** Use negative `margin-top` overlapping, varied image aspect ratios (e.g., 4:3 next to 16:9), left-aligned headers over center-aligned data.
* **8-10 (Asymmetric):** Masonry layouts, CSS Grid with fractional units (e.g., `grid-template-columns: 2fr 1fr 1fr`), massive empty zones (`padding-left: 20vw`).
* **MOBILE OVERRIDE:** For levels 4-10, any asymmetric layout above `768px` MUST aggressively fall back to a strict, single-column layout (`width: 100%`, `padding-inline: 1rem`, `padding-block: 2rem`) on viewports `< 768px` to prevent horizontal scrolling and layout breakage.

### MOTION_INTENSITY (Level 1-10)
* **1-3 (Static):** No automatic animations. CSS `:hover` and `:active` states only.
* **4-7 (Fluid Svelte):** Use `transition` property with `cubic-bezier(0.16, 1, 0.3, 1)` timing. Use `animation-delay` cascades for load-ins via CSS custom property `--delay`. Focus strictly on `transform` and `opacity`. Use `will-change: transform` sparingly.
* **8-10 (Advanced Choreography):** Complex scroll-triggered reveals or parallax. Use Svelte actions wrapping `IntersectionObserver`. Use `spring()` from `svelte/motion` for physics-based interactive elements. NEVER use `window.addEventListener('scroll')`.

### VISUAL_DENSITY (Level 1-10)
* **1-3 (Art Gallery Mode):** Lots of white space. Huge section gaps. Everything feels very expensive and clean.
* **4-7 (Daily App Mode):** Normal spacing for standard web apps.
* **8-10 (Cockpit Mode):** Tiny paddings. No card boxes; just 1px lines to separate data. Everything is packed. **Mandatory:** Use Monospace (`font-family: var(--font-mono)`) for all numbers.

## 7. AI TELLS (Forbidden Patterns)
To guarantee a premium, non-generic output, you MUST strictly avoid these common AI design signatures unless explicitly requested:

### Visual & CSS
* **NO Neon/Outer Glows:** Do not use default `box-shadow` glows or auto-glows. Use inner borders or subtle tinted shadows.
* **NO Pure Black:** Never use `#000000`. Use Off-Black, Zinc-950, or Charcoal.
* **NO Oversaturated Accents:** Desaturate accents to blend elegantly with neutrals.
* **NO Excessive Gradient Text:** Do not use text-fill gradients for large headers.
* **NO Custom Mouse Cursors:** They are outdated and ruin performance/accessibility.
* **NO Tailwind CSS:** Do not use utility classes. Use scoped CSS with CSS custom properties.

### Typography
* **NO Inter Font:** Banned. Use `Geist`, `Outfit`, `Cabinet Grotesk`, or `Satoshi`.
* **NO Oversized H1s:** The first heading should not scream. Control hierarchy with weight and color, not just massive scale.
* **Serif Constraints:** Use Serif fonts ONLY for creative/editorial designs. **NEVER** use Serif on clean Dashboards.

### Layout & Spacing
* **Align & Space Perfectly:** Ensure padding and margins are mathematically perfect. Avoid floating elements with awkward gaps.
* **NO 3-Column Card Layouts:** The generic "3 equal cards horizontally" feature row is BANNED. Use a 2-column Zig-Zag, asymmetric grid, or horizontal scrolling approach instead.

### Content & Data (The "Jane Doe" Effect)
* **NO Generic Names:** "John Doe", "Sarah Chan", or "Jack Su" are banned. Use highly creative, realistic-sounding names.
* **NO Generic Avatars:** DO NOT use standard SVG "egg" or default user icons for avatars. Use creative, believable photo placeholders or specific styling.
* **NO Fake Numbers:** Avoid predictable outputs like `99.99%`, `50%`, or basic phone numbers (`1234567`). Use organic, messy data (`47.2%`, `+1 (312) 847-1928`).
* **NO Startup Slop Names:** "Acme", "Nexus", "SmartFlow". Invent premium, contextual brand names.
* **NO Filler Words:** Avoid AI copywriting clichés like "Elevate", "Seamless", "Unleash", or "Next-Gen". Use concrete verbs.

### External Resources & Components
* **NO Broken Unsplash Links:** Do not use Unsplash. Use absolute, reliable placeholders like `https://picsum.photos/seed/{random_string}/800/600` or SVG UI Avatars.
* **Production-Ready Cleanliness:** Code must be extremely clean, visually striking, memorable, and meticulously refined in every detail.

## 8. THE CREATIVE ARSENAL (High-End Inspiration)
Do not default to generic UI. Pull from this library of advanced concepts to ensure the output is visually striking and memorable. When appropriate, leverage **GSAP (ScrollTrigger/Parallax)** for complex scrolltelling or **ThreeJS/WebGL** for 3D/Canvas animations, rather than basic CSS motion. **CRITICAL:** Never mix GSAP/ThreeJS with Svelte transitions in the same component tree. Default to Svelte's built-in `svelte/transition` + `svelte/motion` for UI interactions. Use GSAP/ThreeJS EXCLUSIVELY for isolated full-page scrolltelling or canvas backgrounds, wrapped in strict `$effect` cleanup.

### The Standard Hero Paradigm
* Stop doing centered text over a dark image. Try asymmetric Hero sections: Text cleanly aligned to the left or right. The background should feature a high-quality, relevant image with a subtle stylistic fade (darkening or lightening gracefully into the background color depending on if it is Light or Dark mode).

### Navigation & Menus
* **Mac OS Dock Magnification:** Nav-bar at the edge; icons scale fluidly on hover.
* **Magnetic Button:** Buttons that physically pull toward the cursor (via `spring()` store).
* **Gooey Menu:** Sub-items detach from the main button like a viscous liquid.
* **Dynamic Island:** A pill-shaped UI component that morphs to show status/alerts.
* **Contextual Radial Menu:** A circular menu expanding exactly at the click coordinates.
* **Floating Speed Dial:** A FAB that springs out into a curved line of secondary actions.
* **Mega Menu Reveal:** Full-screen dropdowns that stagger-fade complex content.

### Layout & Grids
* **Bento Grid:** Asymmetric, tile-based grouping (e.g., Apple Control Center).
* **Masonry Layout:** Staggered grid without fixed row heights (e.g., Pinterest).
* **Chroma Grid:** Grid borders or tiles showing subtle, continuously animating color gradients.
* **Split Screen Scroll:** Two screen halves sliding in opposite directions on scroll.
* **Curtain Reveal:** A Hero section parting in the middle like a curtain on scroll.

### Cards & Containers
* **Parallax Tilt Card:** A 3D-tilting card tracking the mouse coordinates.
* **Spotlight Border Card:** Card borders that illuminate dynamically under the cursor.
* **Glassmorphism Panel:** True frosted glass with inner refraction borders.
* **Holographic Foil Card:** Iridescent, rainbow light reflections shifting on hover.
* **Tinder Swipe Stack:** A physical stack of cards the user can swipe away.
* **Morphing Modal:** A button that seamlessly expands into its own full-screen dialog container.

### Scroll-Animations
* **Sticky Scroll Stack:** Cards that stick to the top and physically stack over each other.
* **Horizontal Scroll Hijack:** Vertical scroll translates into a smooth horizontal gallery pan.
* **Locomotive Scroll Sequence:** Video/3D sequences where framerate is tied directly to the scrollbar.
* **Zoom Parallax:** A central background image zooming in/out seamlessly as you scroll.
* **Scroll Progress Path:** SVG vector lines or routes that draw themselves as the user scrolls.
* **Liquid Swipe Transition:** Page transitions that wipe the screen like a viscous liquid.

### Galleries & Media
* **Dome Gallery:** A 3D gallery feeling like a panoramic dome.
* **Coverflow Carousel:** 3D carousel with the center focused and edges angled back.
* **Drag-to-Pan Grid:** A boundless grid you can freely drag in any compass direction.
* **Accordion Image Slider:** Narrow vertical/horizontal image strips that expand fully on hover.
* **Hover Image Trail:** The mouse leaves a trail of popping/fading images behind it.
* **Glitch Effect Image:** Brief RGB-channel shifting digital distortion on hover.

### Typography & Text
* **Kinetic Marquee:** Endless text bands that reverse direction or speed up on scroll.
* **Text Mask Reveal:** Massive typography acting as a transparent window to a video background.
* **Text Scramble Effect:** Matrix-style character decoding on load or hover.
* **Circular Text Path:** Text curved along a spinning circular path.
* **Gradient Stroke Animation:** Outlined text with a gradient continuously running along the stroke.
* **Kinetic Typography Grid:** A grid of letters dodging or rotating away from the cursor.

### Micro-Interactions & Effects
* **Particle Explosion Button:** CTAs that shatter into particles upon success.
* **Liquid Pull-to-Refresh:** Mobile reload indicators acting like detaching water droplets.
* **Skeleton Shimmer:** Shifting light reflections moving across placeholder boxes.
* **Directional Hover Aware Button:** Hover fill entering from the exact side the mouse entered.
* **Ripple Click Effect:** Visual waves rippling precisely from the click coordinates.
* **Animated SVG Line Drawing:** Vectors that draw their own contours in real time.
* **Mesh Gradient Background:** Organic, lava-lamp-like animated color blobs.
* **Lens Blur Depth:** Dynamic focus blurring background UI layers to highlight a foreground action.

## 9. THE "MOTION-ENGINE" BENTO PARADIGM
When generating modern SaaS dashboards or feature sections, you MUST utilize the following "Bento 2.0" architecture and motion philosophy. This goes beyond static cards and enforces a "Vercel-core meets Dribbble-clean" aesthetic heavily reliant on perpetual physics.

### A. Core Design Philosophy
* **Aesthetic:** High-end, minimal, and functional.
* **Palette:** Background in `#f9fafb`. Cards are pure white (`#ffffff`) with a 1px border of `border: 1px solid rgba(226,232,240,0.5)`.
* **Surfaces:** Use `border-radius: 2.5rem` for all major containers. Apply a "diffusion shadow" (a very light, wide-spreading shadow, e.g., `box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05)`) to create depth without clutter.
* **Typography:** Strict `Geist`, `Satoshi`, or `Cabinet Grotesk` font stack. Use subtle tracking (`letter-spacing: -0.01em`) for headers.
* **Labels:** Titles and descriptions must be placed **outside and below** the cards to maintain a clean, gallery-style presentation.
* **Pixel-Perfection:** Use generous `padding: 2rem` or `2.5rem` padding inside cards.

### B. The Animation Engine Specs (Perpetual Motion)
All cards must contain **"Perpetual Micro-Interactions."** Use the following Svelte-native principles:
* **Spring Physics:** No linear easing. Use `spring()` from `svelte/motion` with `{ stiffness: 100, damping: 20 }` for a premium, weighty feel.
* **Layout Transitions:** Use `animate:flip` on keyed `{#each}` blocks for smooth re-ordering, resizing, and position transitions when data changes.
* **Infinite Loops:** Every card must have an "Active State" that loops infinitely (Pulse, Typewriter, Float, or Carousel) via CSS `@keyframes` to ensure the dashboard feels "alive".
* **Performance:** Wrap dynamic lists with `animate:flip` and optimize for 60fps. **PERFORMANCE CRITICAL:** Any perpetual motion or infinite loop should be CSS-based (`@keyframes`) when possible, and isolated in its own `.svelte` leaf component with clean `$effect` cleanup when JS-driven. Svelte compiles to surgical DOM updates — no virtual DOM overhead.

### C. The 5-Card Archetypes (Micro-Animation Specs)
Implement these specific micro-animations when constructing Bento grids (e.g., Row 1: 3 cols | Row 2: 2 cols split 70/30):
1. **The Intelligent List:** A vertical stack of items with an infinite auto-sorting loop. Items swap positions using `animate:flip` on a keyed `{#each}`, simulating an AI prioritizing tasks in real-time.
2. **The Command Input:** A search/AI bar with a multi-step Typewriter Effect. It cycles through complex prompts, including a blinking cursor and a "processing" state with a shimmering loading gradient.
3. **The Live Status:** A scheduling interface with "breathing" status indicators. Include a pop-up notification badge that emerges with a scale overshoot via `spring()`, stays for 3 seconds, and vanishes with `transition:fade`.
4. **The Wide Data Stream:** A horizontal "Infinite Carousel" of data cards or metrics. Ensure the loop is seamless with CSS `@keyframes translateX` animation on the inner track.
5. **The Contextual UI (Focus Mode):** A document view that animates a staggered highlight of a text block, followed by a `transition:fly` of a floating action toolbar with micro-icons.

## 10. FINAL PRE-FLIGHT CHECK
Evaluate your code against this matrix before output. This is the **last** filter you apply to your logic.
- [ ] Is global state in `.svelte.ts` modules where appropriate, avoiding deep prop-drilling?
- [ ] Is mobile layout collapse (`width: 100%`, `padding-inline: 1rem`, `max-width: 1400px; margin-inline: auto`) guaranteed for high-variance designs?
- [ ] Do full-height sections safely use `min-height: 100dvh` instead of the bugged `height: 100vh`?
- [ ] Do `$effect` animations contain strict cleanup functions (`return () => cleanup()`)?
- [ ] Are empty, loading, and error states provided?
- [ ] Are cards omitted in favor of spacing where possible?
- [ ] Are CPU-heavy perpetual animations isolated in their own `.svelte` leaf components?
- [ ] Is all CSS scoped in `<style>` blocks using CSS custom properties — no Tailwind utility classes?
- [ ] Are Svelte's built-in transitions (`svelte/transition`, `svelte/animate`, `svelte/motion`) used as the primary animation approach?
