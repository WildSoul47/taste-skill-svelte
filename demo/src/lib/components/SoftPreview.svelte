<script lang="ts">
	let mouseX = $state(50);
	let mouseY = $state(50);
	let hovered = $state(false);

	function handleMouseMove(e: MouseEvent) {
		const rect = (e.currentTarget as HTMLElement).getBoundingClientRect();
		mouseX = ((e.clientX - rect.left) / rect.width) * 100;
		mouseY = ((e.clientY - rect.top) / rect.height) * 100;
	}
</script>

<div
	class="glass-panel"
	class:hovered
	onmousemove={handleMouseMove}
	onmouseenter={() => hovered = true}
	onmouseleave={() => { hovered = false; mouseX = 50; mouseY = 50; }}
	style="--mx: {mouseX}%; --my: {mouseY}%;"
>
	<div class="glass-orb"></div>
	<div class="glass-content">
		<div class="glass-badge">Premium Agency</div>
		<div class="glass-amount">$150k</div>
		<div class="glass-desc">Double-bezel architecture with nested CTA pills</div>
	</div>
	<div class="glass-border-light"></div>
</div>

<style>
	.glass-panel {
		position: relative;
		border-radius: 1.5rem;
		padding: 2rem;
		background: rgba(5, 5, 5, 0.85);
		border: 1px solid rgba(255, 255, 255, 0.08);
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06);
		overflow: hidden;
		transform: scale(1);
		transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
		cursor: default;
	}

	.glass-panel.hovered {
		transform: scale(1.02);
	}

	.glass-orb {
		position: absolute;
		width: 200px;
		height: 200px;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(37, 99, 235, 0.5) 0%, transparent 70%);
		left: calc(var(--mx) * 1%);
		top: calc(var(--my) * 1%);
		transform: translate(-50%, -50%);
		filter: blur(40px);
		transition: left 0.4s ease, top 0.4s ease;
		pointer-events: none;
	}

	.glass-content {
		position: relative;
		z-index: 1;
	}

	.glass-badge {
		display: inline-block;
		font-size: 0.6rem;
		font-weight: 600;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: rgba(255, 255, 255, 0.4);
		border: 1px solid rgba(255, 255, 255, 0.1);
		padding: 0.3rem 0.8rem;
		border-radius: 100px;
		margin-bottom: 1.25rem;
	}

	.glass-amount {
		font-size: 2.5rem;
		font-weight: 800;
		letter-spacing: -0.03em;
		color: #F9FAFB;
		line-height: 1;
		margin-bottom: 0.5rem;
	}

	.glass-desc {
		font-size: 0.8rem;
		color: rgba(255, 255, 255, 0.35);
		line-height: 1.5;
	}

	.glass-border-light {
		position: absolute;
		inset: 0;
		border-radius: 1.5rem;
		border: 1px solid rgba(255, 255, 255, 0.04);
		pointer-events: none;
	}
</style>
