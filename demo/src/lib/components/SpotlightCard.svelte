<script lang="ts">
	let { x = 0, y = 0 }: { x: number; y: number } = $props();
</script>

<div class="spotlight" style="--mx: {x}%; --my: {y}%;">
	<div class="spotlight-ring"></div>
	<div class="spotlight-grid">
		{#each Array(12) as _, i}
			<div class="grid-dot" style="--i: {i};"></div>
		{/each}
	</div>
	<div class="spotlight-label">Spring Physics</div>
</div>

<style>
	.spotlight {
		position: relative;
		width: 100%;
		aspect-ratio: 16/10;
		border-radius: var(--radius-lg);
		background: #0A0A0A;
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.spotlight-ring {
		position: absolute;
		width: 60%;
		aspect-ratio: 1;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(37, 99, 235, 0.3) 0%, transparent 70%);
		left: calc(var(--mx) * 1%);
		top: calc(var(--my) * 1%);
		transform: translate(-50%, -50%);
		transition: left 0.3s ease, top 0.3s ease;
		filter: blur(30px);
	}

	.spotlight-grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 0.75rem;
		padding: 1.5rem;
		position: relative;
		z-index: 1;
	}

	.grid-dot {
		width: 2rem;
		height: 2rem;
		border-radius: 50%;
		background: rgba(255, 255, 255, 0.08);
		border: 1px solid rgba(255, 255, 255, 0.06);
		animation: pulse-dot 3s ease-in-out infinite;
		animation-delay: calc(var(--i) * 0.15s);
	}

	.spotlight-label {
		position: absolute;
		bottom: 1rem;
		left: 1.5rem;
		font-size: 0.65rem;
		font-weight: 500;
		letter-spacing: 0.15em;
		text-transform: uppercase;
		color: rgba(255, 255, 255, 0.3);
	}

	@keyframes pulse-dot {
		0%, 100% { transform: scale(1); opacity: 1; }
		50% { transform: scale(0.7); opacity: 0.4; }
	}
</style>
