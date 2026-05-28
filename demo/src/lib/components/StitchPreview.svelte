<script lang="ts">
	import { onMount } from 'svelte';

	let activeSwatch = $state(0);

	const tokens = [
		{ name: 'Canvas', hex: '#F9FAFB', textColor: '#18181B' },
		{ name: 'Surface', hex: '#FFFFFF', textColor: '#18181B' },
		{ name: 'Text', hex: '#18181B', textColor: '#F9FAFB' },
		{ name: 'Accent', hex: '#2563EB', textColor: '#FFFFFF' },
		{ name: 'Border', hex: '#E2E8F0', textColor: '#18181B' },
		{ name: 'Muted', hex: '#71717A', textColor: '#FFFFFF' }
	];

	onMount(() => {
		const interval = setInterval(() => {
			activeSwatch = (activeSwatch + 1) % tokens.length;
		}, 1800);
		return () => clearInterval(interval);
	});
</script>

<div class="palette">
	<div class="palette-header">
		<span class="palette-title">Design Tokens</span>
		<span class="palette-badge">6 tokens</span>
	</div>
	<div class="swatches">
		{#each tokens as token, i}
			<button
				class="swatch"
				class:active={activeSwatch === i}
				onclick={() => activeSwatch = i}
				aria-label="{token.name}: {token.hex}"
			>
				<div class="swatch-color" style="background: {token.hex};"></div>
				<span class="swatch-name">{token.name}</span>
				<span class="swatch-hex" style="color: {activeSwatch === i ? token.hex : 'inherit'};">{token.hex}</span>
			</button>
		{/each}
	</div>
	<div class="palette-footer">
		<span class="palette-font">Aa</span>
		<span class="palette-font-label">Outfit 700</span>
		<span class="palette-font-sample">The quick brown fox</span>
	</div>
</div>

<style>
	.palette {
		border: 1px solid var(--color-border);
		border-radius: var(--radius-md);
		padding: 1rem;
		background: var(--color-surface);
	}

	.palette-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 0.75rem;
	}

	.palette-title {
		font-size: 0.75rem;
		font-weight: 600;
		color: var(--color-text);
		letter-spacing: -0.01em;
	}

	.palette-badge {
		font-size: 0.55rem;
		font-weight: 500;
		padding: 0.15rem 0.5rem;
		border-radius: 100px;
		background: #F0FDF4;
		color: #346538;
		border: 1px solid #BBF7D0;
	}

	.swatches {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 0.5rem;
		margin-bottom: 1rem;
	}

	.swatch {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 0.3rem;
		padding: 0.6rem 0.4rem;
		border-radius: 8px;
		border: 1.5px solid transparent;
		background: transparent;
		cursor: pointer;
		transition: border-color 0.2s ease, background 0.2s ease;
		font-family: inherit;
	}

	.swatch.active {
		border-color: var(--color-accent);
		background: #F0F7FF;
	}

	.swatch-color {
		width: 28px;
		height: 28px;
		border-radius: 6px;
		border: 1px solid rgba(0, 0, 0, 0.06);
		transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.swatch.active .swatch-color {
		transform: scale(1.15);
	}

	.swatch-name {
		font-size: 0.55rem;
		font-weight: 500;
		color: var(--color-text);
		letter-spacing: 0.02em;
	}

	.swatch-hex {
		font-size: 0.5rem;
		font-weight: 500;
		color: var(--color-text-muted);
		font-variant-numeric: tabular-nums;
		transition: color 0.2s ease;
	}

	.palette-footer {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		padding-top: 0.75rem;
		border-top: 1px solid var(--color-border);
	}

	.palette-font {
		font-size: 1.1rem;
		font-weight: 700;
		color: var(--color-text);
		line-height: 1;
	}

	.palette-font-label {
		font-size: 0.55rem;
		font-weight: 500;
		color: var(--color-text-muted);
	}

	.palette-font-sample {
		font-size: 0.6rem;
		color: var(--color-text-muted);
		overflow: hidden;
		white-space: nowrap;
		animation: type-reveal 4s steps(20) infinite;
		border-right: 1px solid var(--color-text-muted);
	}

	@keyframes type-reveal {
		0%, 10% { width: 0; }
		50%, 70% { width: 100%; }
		90%, 100% { width: 0; }
	}
</style>
