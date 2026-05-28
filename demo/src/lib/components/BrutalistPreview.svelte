<script lang="ts">
	import { onMount } from 'svelte';

	let active = $state(0);
	const items = ['BRUTALIST', 'SWISS INDUSTRIAL', 'TACTICAL CRT', 'HALFTONE FX'];

	onMount(() => {
		const interval = setInterval(() => {
			active = (active + 1) % items.length;
		}, 2200);
		return () => clearInterval(interval);
	});
</script>

<div class="brutalist-frame">
	<div class="frame-header">
		<span class="frame-id">UNIT / SK-04</span>
		<span class="frame-rev">REV 2.6</span>
	</div>
	<div class="frame-body">
		<div class="frame-display">
			{#each items as item, i}
				<span class="frame-text" class:active={active === i}>{item}</span>
			{/each}
		</div>
		<div class="frame-scanlines"></div>
		<div class="frame-accent"></div>
	</div>
	<div class="frame-footer">
		<span>CROSSHAIR: ACTIVE</span>
		<span>STATUS: ONLINE</span>
	</div>
</div>

<style>
	.brutalist-frame {
		border: 2px solid #E61919;
		padding: 0;
		position: relative;
		background: #0A0A0A;
		color: #EAEAEA;
		overflow: hidden;
	}

	.frame-header, .frame-footer {
		display: flex;
		justify-content: space-between;
		padding: 0.5rem 1rem;
		font-size: 0.6rem;
		letter-spacing: 0.15em;
		text-transform: uppercase;
		color: rgba(234, 234, 234, 0.4);
		border-bottom: 1px solid rgba(230, 25, 25, 0.2);
	}

	.frame-footer {
		border-bottom: none;
		border-top: 1px solid rgba(230, 25, 25, 0.2);
	}

	.frame-id, .frame-rev {
		font-variant-numeric: tabular-nums;
	}

	.frame-body {
		position: relative;
		padding: 2.5rem 1.5rem;
		min-height: 120px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.frame-display {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.frame-text {
		font-size: clamp(1.2rem, 3vw, 1.8rem);
		font-weight: 800;
		letter-spacing: -0.02em;
		text-transform: uppercase;
		color: #E61919;
		position: absolute;
		opacity: 0;
		transform: translateY(8px);
		transition: opacity 0.4s ease, transform 0.4s ease;
	}

	.frame-text.active {
		opacity: 1;
		transform: translateY(0);
	}

	.frame-scanlines {
		position: absolute;
		inset: 0;
		background: repeating-linear-gradient(
			0deg,
			transparent,
			transparent 2px,
			rgba(0, 0, 0, 0.15) 2px,
			rgba(0, 0, 0, 0.15) 4px
		);
		pointer-events: none;
	}

	.frame-accent {
		position: absolute;
		top: 0.75rem;
		right: 0.75rem;
		width: 0.5rem;
		height: 0.5rem;
		background: #4AF626;
		border-radius: 0;
		animation: blink 2s step-end infinite;
	}

	@keyframes blink {
		0%, 100% { opacity: 1; }
		50% { opacity: 0; }
	}
</style>
