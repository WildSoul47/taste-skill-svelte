<script lang="ts">
	import { onMount } from 'svelte';
	import SpotlightCard from '$lib/components/SpotlightCard.svelte';
	import BrutalistPreview from '$lib/components/BrutalistPreview.svelte';
	import MinimalistPreview from '$lib/components/MinimalistPreview.svelte';
	import SoftPreview from '$lib/components/SoftPreview.svelte';
	import RedesignPreview from '$lib/components/RedesignPreview.svelte';
	import OutputPreview from '$lib/components/OutputPreview.svelte';
	import StitchPreview from '$lib/components/StitchPreview.svelte';

	let visibleCards = $state<Set<number>>(new Set());
	let cardEls: HTMLDivElement[] = [];
	let heroVisible = $state(false);
	let mousePos = $state({ x: 50, y: 50 });

	interface Skill {
		slug: string;
		name: string;
		tagline: string;
		description: string;
		dials: string;
		color: string;
		darkColor: string;
		icon: string;
		preview: 'spotlight' | 'brutalist' | 'minimalist' | 'soft' | 'stitch' | 'redesign' | 'output';
	}

	const skills: Skill[] = [
		{
			slug: 'taste',
			name: 'Taste',
			tagline: 'The flagship design skill',
			description: '3-dial configuration, 50+ creative patterns, spring physics, and a strict anti-slop checklist for SvelteKit.',
			dials: 'V:8  M:6  D:4',
			color: '#1A1A1A',
			darkColor: '#F7F6F3',
			icon: 'T',
			preview: 'spotlight'
		},
		{
			slug: 'soft',
			name: 'Soft',
			tagline: 'Premium agency aesthetic',
			description: 'Double-bezel architecture, glassmorphism panels, and three vibe archetypes from Ethereal Glass to Editorial Luxury.',
			dials: 'V:8  M:7  D:3',
			color: '#0A0A0A',
			darkColor: '#E2E8F0',
			icon: 'S',
			preview: 'soft'
		},
		{
			slug: 'minimalist',
			name: 'Minimalist',
			tagline: 'Warm editorial clarity',
			description: 'Muted pastel accents, flat bento grids, and faux-OS window chrome. Zero gradients, zero heavy shadows.',
			dials: 'V:4  M:2  D:5',
			color: '#2F3437',
			darkColor: '#F7F6F3',
			icon: 'M',
			preview: 'minimalist'
		},
		{
			slug: 'brutalist',
			name: 'Brutalist',
			tagline: 'Industrial mechanical',
			description: 'Swiss Industrial Print or Tactical CRT Terminal. Extreme type scale, aviation red, zero border-radius.',
			dials: 'V:9  M:4  D:7',
			color: '#C41818',
			darkColor: '#F4F4F0',
			icon: 'B',
			preview: 'brutalist'
		},
		{
			slug: 'stitch',
			name: 'Stitch',
			tagline: 'Google Stitch integration',
			description: 'Semantic DESIGN.md files as single source of truth. Inline image typography, touch-target specs, serif-ban enforcement.',
			dials: 'V:8  M:6  D:4',
			color: '#1A1A1A',
			darkColor: '#F7F6F3',
			icon: 'St',
			preview: 'stitch'
		},
		{
			slug: 'redesign',
			name: 'Redesign',
			tagline: 'Systematic audit',
			description: '90-item checklist across typography, color, layout, interactivity. Fix priority ranking for existing SvelteKit projects.',
			dials: 'Process',
			color: '#2D5A27',
			darkColor: '#EDF3EC',
			icon: 'R',
			preview: 'redesign'
		},
		{
			slug: 'output',
			name: 'Output',
			tagline: 'Zero truncation',
			description: 'Framework-agnostic completeness enforcement. Bans placeholders, mandates cross-check, handles token splits cleanly.',
			dials: 'Process',
			color: '#8B3A2F',
			darkColor: '#FDEBEC',
			icon: 'O',
			preview: 'output'
		}
	];

	const dialDefs = [
		{ name: 'DESIGN_VARIANCE', value: 8, low: 'Predictable', high: 'Asymmetric', desc: 'Layout predictability. At 8: asymmetric grids, massive empty zones, offset compositions.' },
		{ name: 'MOTION_INTENSITY', value: 6, low: 'Static', high: 'Cinematic', desc: 'Animation depth. At 6: fluid transitions, staggered reveals, spring physics.' },
		{ name: 'VISUAL_DENSITY', value: 4, low: 'Gallery', high: 'Cockpit', desc: 'Information density. At 4: generous whitespace, art gallery breathing room.' }
	];

	onMount(() => {
		heroVisible = true;

		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						const idx = Number(entry.target.getAttribute('data-index'));
						visibleCards = new Set([...visibleCards, idx]);
					}
				}
			},
			{ threshold: 0.08 }
		);

		for (const el of cardEls) {
			if (el) observer.observe(el);
		}

		return () => observer.disconnect();
	});

	function handleHeroMouse(e: MouseEvent) {
		const rect = (e.currentTarget as HTMLElement).getBoundingClientRect();
		mousePos = {
			x: ((e.clientX - rect.left) / rect.width) * 100,
			y: ((e.clientY - rect.top) / rect.height) * 100
		};
	}
</script>

<svelte:head>
	<title>taste-skill-svelte</title>
	<meta name="description" content="7 AI design skills for SvelteKit. No Tailwind. No Inter. No slop." />
</svelte:head>

<main>
	<!-- Hero -->
	<section class="hero" onmousemove={handleHeroMouse}>
		<div class="hero-inner" class:hero-visible={heroVisible}>
			<div class="hero-eyebrow">Svelte 5 Skill Collection</div>
			<h1 class="hero-title">
				<span class="hero-line">taste-skill</span><span class="hero-accent">-svelte</span>
			</h1>
			<p class="hero-sub">
				Seven design skills, ported to SvelteKit with scoped CSS and spring physics.
				No Tailwind. No Inter. No slop.
			</p>
			<div class="hero-cta">
				<a href="#skills" class="cta-primary">Explore skills</a>
				<a href="#install" class="cta-secondary">Install</a>
			</div>
		</div>
		<div class="hero-decor" aria-hidden="true">
			<div class="decor-orb" style="left: {mousePos.x * 0.2 + 65}%; top: {mousePos.y * 0.2 + 20}%;"></div>
		</div>
	</section>

	<!-- Skills -->
	<section class="section" id="skills">
		<div class="section-header">
			<div class="section-eyebrow">Skill Arsenal</div>
			<h2 class="section-title"><em>Seven</em> skills, one philosophy</h2>
			<p class="section-desc">Each card ships with a live visual preview. Hover, click, and explore.</p>
		</div>
		<div class="skills-grid">
			{#each skills as skill, i}
				<div
					class="skill-card"
					class:visible={visibleCards.has(i)}
					class:span-2={skill.slug === 'taste'}
					style="--card-color: {skill.color}; --delay: {i * 80}ms;"
					bind:this={cardEls[i]}
					data-index={i}
				>
					<div class="card-top">
						<div class="card-info">
							<div class="card-header">
								<div class="card-icon" style="background: {skill.color}; color: {skill.darkColor};">
									{skill.icon}
								</div>
								<span class="card-dials">{skill.dials}</span>
							</div>
							<h3 class="card-name">{skill.name}</h3>
							<p class="card-tagline" style="color: {skill.color};">{skill.tagline}</p>
							<p class="card-desc">{skill.description}</p>
						</div>
						<div class="card-preview">
							{#if skill.preview === 'spotlight'}
								<SpotlightCard x={mousePos.x} y={mousePos.y} />
							{:else if skill.preview === 'soft'}
								<SoftPreview />
							{:else if skill.preview === 'minimalist'}
								<MinimalistPreview />
							{:else if skill.preview === 'brutalist'}
								<BrutalistPreview />
							{:else if skill.preview === 'stitch'}
								<StitchPreview />
							{:else if skill.preview === 'redesign'}
								<RedesignPreview />
							{:else if skill.preview === 'output'}
								<OutputPreview />
							{/if}
						</div>
					</div>
					<div class="card-footer">
						<span class="card-slug">{skill.slug}-skill</span>
						<span class="card-arrow">&rarr;</span>
					</div>
				</div>
			{/each}
		</div>
	</section>

	<!-- Dials -->
	<section class="section section--alt">
		<div class="section-header">
			<div class="section-eyebrow">Configuration</div>
			<h2 class="section-title">Three dials, <em>infinite</em> range</h2>
			<p class="section-desc">Every skill responds to the same three-dimensional configuration system.</p>
		</div>
		<div class="dials-grid">
			{#each dialDefs as dial, i}
				<div class="dial-card" style="--delay: {i * 120}ms;">
					<div class="dial-top">
						<span class="dial-low">{dial.low}</span>
						<span class="dial-val">{dial.value}</span>
						<span class="dial-high">{dial.high}</span>
					</div>
					<div class="dial-track">
						<div class="dial-fill" style="width: {dial.value * 10}%;"></div>
					</div>
					<h3 class="dial-name">{dial.name}</h3>
					<p class="dial-desc">{dial.desc}</p>
				</div>
			{/each}
		</div>
	</section>

	<!-- Why -->
	<section class="section">
		<div class="section-header">
			<div class="section-eyebrow">Why This Exists</div>
			<h2 class="section-title">Built to fight <em>AI slop</em></h2>
		</div>
		<div class="features-grid">
			<div class="feature-item">
				<span class="feature-num">01</span>
				<div>
					<h4 class="feature-title">Scoped CSS, not utility classes</h4>
					<p class="feature-desc">Design tokens as CSS custom properties. Zero abstraction layer. No version conflicts.</p>
				</div>
			</div>
			<div class="feature-item">
				<span class="feature-num">02</span>
				<div>
					<h4 class="feature-title">Spring physics by default</h4>
					<p class="feature-desc">Every interaction uses calibrated stiffness and damping. No linear easing.</p>
				</div>
			</div>
			<div class="feature-item">
				<span class="feature-num">03</span>
				<div>
					<h4 class="feature-title">Anti-pattern enforcement</h4>
					<p class="feature-desc">Inter banned. Purple glows banned. 3-column cards banned. Generic names banned.</p>
				</div>
			</div>
			<div class="feature-item">
				<span class="feature-num">04</span>
				<div>
					<h4 class="feature-title">Perpetual micro-motion</h4>
					<p class="feature-desc">CSS keyframe loops for ambient animation. Staggered orchestration via custom properties.</p>
				</div>
			</div>
		</div>
	</section>

	<!-- Install -->
	<section class="section" id="install">
		<div class="install-card">
			<div class="install-eyebrow">Get Started</div>
			<div class="install-code">
				<code>npx skills add https://github.com/WildSoul47/taste-skill-svelte</code>
			</div>
			<p class="install-note">Installs to .claude/skills/. Works with Claude, Cursor, Gemini, and Copilot.</p>
		</div>
	</section>

	<footer class="site-footer">
		<p>Ported from <strong>taste-skill</strong> by Leonxlnx. Svelte 5 adaptation.</p>
	</footer>
</main>

<style>
	/* ===== Hero ===== */
	.hero {
		position: relative;
		min-height: 100dvh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 4rem 2rem;
		overflow: hidden;
	}

	.hero-inner {
		position: relative;
		z-index: 2;
		max-width: 64rem;
		text-align: center;
		opacity: 0;
		transform: translateY(24px);
		transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.hero-inner.hero-visible {
		opacity: 1;
		transform: translateY(0);
	}

	.hero-eyebrow {
		font-size: 0.7rem;
		font-weight: 600;
		letter-spacing: 0.18em;
		text-transform: uppercase;
		color: var(--color-accent);
		margin-bottom: 1.75rem;
	}

	.hero-title {
		font-size: clamp(3rem, 8vw, 5.5rem);
		font-weight: 800;
		line-height: 1;
		letter-spacing: -0.03em;
		margin-bottom: 1.75rem;
	}

	.hero-line { display: block; }

	.hero-accent {
		color: var(--color-accent);
		font-family: var(--font-serif);
		font-style: italic;
		font-weight: 400;
	}

	.hero-sub {
		font-size: 1.05rem;
		color: var(--color-text-muted);
		line-height: 1.7;
		max-width: 36ch;
		margin-inline: auto;
		margin-bottom: 2.5rem;
	}

	.hero-cta {
		display: flex;
		gap: 0.75rem;
		justify-content: center;
	}

	.cta-primary {
		font-size: 0.85rem;
		font-weight: 600;
		padding: 0.65rem 1.5rem;
		border-radius: var(--radius-sm);
		background: var(--color-text);
		color: var(--color-canvas);
		transition: opacity 0.2s ease;
	}

	.cta-primary:hover { opacity: 0.85; }

	.cta-secondary {
		font-size: 0.85rem;
		font-weight: 500;
		padding: 0.65rem 1.5rem;
		border-radius: var(--radius-sm);
		border: 1px solid var(--color-border);
		color: var(--color-text-muted);
		transition: border-color 0.2s ease;
	}

	.cta-secondary:hover { border-color: var(--color-text-muted); }

	/* Decor */
	.hero-decor {
		position: absolute;
		inset: 0;
		z-index: 1;
		pointer-events: none;
	}

	.decor-orb {
		position: absolute;
		width: 35vw;
		height: 35vw;
		max-width: 400px;
		max-height: 400px;
		border-radius: 50%;
		background: var(--color-accent);
		opacity: 0.06;
		filter: blur(60px);
		transition: left 0.8s ease, top 0.8s ease;
	}

	/* ===== Sections ===== */
	.section {
		max-width: 1400px;
		margin-inline: auto;
		padding: 6rem 2rem;
	}

	.section--alt {
		background: var(--color-surface);
		max-width: none;
		padding: 6rem 2rem;
	}

	.section--alt > * {
		max-width: 1400px;
		margin-inline: auto;
	}

	.section-header {
		margin-bottom: 3rem;
	}

	.section-eyebrow {
		font-size: 0.6rem;
		font-weight: 600;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: var(--color-accent);
		margin-bottom: 0.75rem;
	}

	.section-title {
		font-size: clamp(1.75rem, 4vw, 2.5rem);
		font-weight: 800;
		letter-spacing: -0.02em;
		line-height: 1.1;
		margin-bottom: 0.75rem;
	}

	.section-title em {
		font-family: var(--font-serif);
		font-style: italic;
		font-weight: 400;
	}

	.section-desc {
		font-size: 0.95rem;
		color: var(--color-text-muted);
		line-height: 1.6;
		max-width: 44ch;
	}

	/* ===== Skill Cards ===== */
	.skills-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 1.25rem;
	}

	.skill-card {
		background: var(--color-surface);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-xl);
		padding: 1.5rem;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		opacity: 0;
		transform: translateY(20px);
		transition:
			opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1),
			transform 0.6s cubic-bezier(0.16, 1, 0.3, 1),
			box-shadow 0.3s ease;
		transition-delay: var(--delay);
	}

	.skill-card.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.skill-card.visible:hover {
		box-shadow: var(--shadow-diffuse);
		transform: translateY(-2px);
	}

	.skill-card:hover .card-arrow {
		transform: translateX(3px);
	}

	.skill-card.span-2 { grid-column: span 2; }

	.card-top {
		display: flex;
		gap: 1.25rem;
		flex: 1;
	}

	.card-info { flex: 1; min-width: 0; }
	.card-preview { flex: 1; min-width: 0; display: flex; align-items: stretch; }

	.card-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 0.4rem;
	}

	.card-icon {
		width: 2.25rem;
		height: 2.25rem;
		border-radius: var(--radius-sm);
		display: flex;
		align-items: center;
		justify-content: center;
		font-weight: 700;
		font-size: 0.8rem;
	}

	.card-dials {
		font-size: 0.6rem;
		font-weight: 500;
		letter-spacing: 0.05em;
		color: var(--color-text-muted);
		font-variant-numeric: tabular-nums;
	}

	.card-name {
		font-size: 1.25rem;
		font-weight: 700;
		letter-spacing: -0.02em;
		margin-bottom: 0.15rem;
	}

	.card-tagline {
		font-size: 0.75rem;
		font-weight: 500;
		margin-bottom: 0.4rem;
	}

	.card-desc {
		font-size: 0.8rem;
		color: var(--color-text-muted);
		line-height: 1.55;
	}

	.card-footer {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-top: 0.75rem;
		border-top: 1px solid var(--color-border);
	}

	.card-slug {
		font-size: 0.65rem;
		font-weight: 500;
		color: var(--color-text-muted);
	}

	.card-arrow {
		font-size: 0.9rem;
		color: var(--color-text-muted);
		transition: transform 0.3s var(--ease-out-expo);
	}

	/* ===== Dials ===== */
	.dials-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 1.5rem;
	}

	.dial-card {
		padding: 1.5rem;
		border: 1px solid var(--color-border);
		border-radius: var(--radius-lg);
		background: var(--color-canvas);
	}

	.dial-top {
		display: flex;
		justify-content: space-between;
		align-items: baseline;
		margin-bottom: 0.75rem;
	}

	.dial-low, .dial-high {
		font-size: 0.55rem;
		font-weight: 500;
		letter-spacing: 0.1em;
		text-transform: uppercase;
		color: var(--color-text-muted);
	}

	.dial-val {
		font-size: 2.25rem;
		font-weight: 800;
		letter-spacing: -0.03em;
		line-height: 1;
	}

	.dial-track {
		height: 3px;
		background: var(--color-border);
		border-radius: 2px;
		margin-bottom: 1rem;
		position: relative;
	}

	.dial-fill {
		height: 100%;
		background: var(--color-accent);
		border-radius: 2px;
	}

	.dial-name {
		font-size: 0.8rem;
		font-weight: 600;
		letter-spacing: 0.03em;
		margin-bottom: 0.3rem;
	}

	.dial-desc {
		font-size: 0.75rem;
		color: var(--color-text-muted);
		line-height: 1.5;
	}

	/* ===== Features ===== */
	.features-grid {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		gap: 0;
	}

	.feature-item {
		display: flex;
		gap: 1.25rem;
		padding: 1.75rem;
		border-bottom: 1px solid var(--color-border);
	}

	.feature-item:nth-child(odd) {
		border-right: 1px solid var(--color-border);
	}

	.feature-num {
		font-size: 0.65rem;
		font-weight: 700;
		color: var(--color-accent);
		padding-top: 0.15rem;
		flex-shrink: 0;
		font-variant-numeric: tabular-nums;
	}

	.feature-title {
		font-size: 0.9rem;
		font-weight: 700;
		letter-spacing: -0.01em;
		margin-bottom: 0.25rem;
	}

	.feature-desc {
		font-size: 0.8rem;
		color: var(--color-text-muted);
		line-height: 1.55;
	}

	/* ===== Install ===== */
	.install-card {
		max-width: 36rem;
		margin-inline: auto;
		border: 1px solid var(--color-border);
		border-radius: var(--radius-xl);
		padding: 2.5rem;
		background: var(--color-surface);
		text-align: center;
	}

	.install-eyebrow {
		font-size: 0.6rem;
		font-weight: 600;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: var(--color-accent);
		margin-bottom: 1.25rem;
		display: block;
	}

	.install-code {
		background: #1A1A1A;
		color: #D4D4D4;
		padding: 1rem 1.5rem;
		border-radius: var(--radius-md);
		font-family: 'Geist Mono', monospace;
		font-size: 0.78rem;
		text-align: left;
		overflow-x: auto;
		margin-bottom: 0.75rem;
	}

	.install-note {
		font-size: 0.75rem;
		color: var(--color-text-muted);
	}

	/* ===== Footer ===== */
	.site-footer {
		text-align: center;
		padding: 3rem 2rem;
		border-top: 1px solid var(--color-border);
	}

	.site-footer p {
		font-size: 0.8rem;
		color: var(--color-text-muted);
	}

	/* ===== Tablet ===== */
	@media (max-width: 1024px) {
		.skills-grid { grid-template-columns: repeat(2, 1fr); }
		.skill-card.span-2 { grid-column: span 2; }
		.dials-grid { grid-template-columns: repeat(2, 1fr); }
		.card-top { flex-direction: column; }
	}

	/* ===== Mobile ===== */
	@media (max-width: 768px) {
		.hero { padding: 3rem 1.5rem; }
		.hero-title { font-size: clamp(2.25rem, 12vw, 3.5rem); }
		.skills-grid { grid-template-columns: 1fr; }
		.skill-card.span-2 { grid-column: span 1; }
		.card-top { flex-direction: column; }
		.dials-grid { grid-template-columns: 1fr; }
		.features-grid { grid-template-columns: 1fr; }
		.feature-item:nth-child(odd) { border-right: none; }
		.section, .section--alt { padding: 3rem 1.5rem; }
	}
</style>
