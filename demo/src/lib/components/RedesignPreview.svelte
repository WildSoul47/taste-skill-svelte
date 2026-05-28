<script lang="ts">
	let active = $state(false);

	function toggle() {
		active = !active;
	}
</script>

<button class="before-after" onclick={toggle} aria-label="Toggle before/after">
	{#if !active}
		<div class="ba-view ba-bad">
			<div class="ba-label-row">
				<span class="ba-label ba-label-bad">Before</span>
				<span class="ba-toggle">Click to fix</span>
			</div>
			<div class="ba-bad-title">Welcome to Our Platform</div>
			<div class="ba-bad-body">We provide seamless solutions to elevate your next-gen experience.</div>
			<div class="ba-bad-btn">Get Started</div>
			<div class="ba-bad-tags">
				<span>99.99% Uptime</span>
				<span>500+ Users</span>
			</div>
		</div>
	{:else}
		<div class="ba-view ba-good">
			<div class="ba-label-row">
				<span class="ba-label ba-label-good">After</span>
				<span class="ba-toggle">Click to compare</span>
			</div>
			<div class="ba-good-eyebrow">Design System</div>
			<div class="ba-good-title">Korsod Praxis</div>
			<div class="ba-good-body">Scoped CSS architecture with calibrated color tokens and spring physics.</div>
			<div class="ba-good-cta">View Audit &rarr;</div>
		</div>
	{/if}
</button>

<style>
	.before-after {
		display: block;
		border: none;
		background: none;
		cursor: pointer;
		width: 100%;
		text-align: left;
		font-family: inherit;
		color: inherit;
		padding: 0;
	}

	.ba-view {
		padding: 1.25rem;
		border-radius: var(--radius-md);
		transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.ba-bad {
		background: #FEF2F2;
		border: 1px solid #FECACA;
	}

	.ba-good {
		background: #F0FDF4;
		border: 1px solid #BBF7D0;
	}

	.ba-label-row {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 0.75rem;
	}

	.ba-label {
		font-size: 0.55rem;
		font-weight: 600;
		letter-spacing: 0.15em;
		text-transform: uppercase;
	}

	.ba-label-bad { color: #9F2F2D; }
	.ba-label-good { color: #346538; }

	.ba-toggle {
		font-size: 0.55rem;
		color: var(--color-text-muted);
		opacity: 0.6;
	}

	/* Bad */
	.ba-bad-title {
		font-size: 0.95rem;
		font-weight: 400;
		color: #1F2937;
		margin-bottom: 0.35rem;
		font-family: Inter, Arial, sans-serif;
	}

	.ba-bad-body {
		font-size: 0.65rem;
		color: #6B7280;
		margin-bottom: 0.5rem;
		line-height: 1.5;
	}

	.ba-bad-btn {
		display: inline-block;
		background: #7C3AED;
		color: white;
		font-size: 0.6rem;
		padding: 0.25rem 0.75rem;
		border-radius: 100px;
		margin-bottom: 0.5rem;
	}

	.ba-bad-tags {
		display: flex;
		gap: 0.35rem;
	}

	.ba-bad-tags span {
		font-size: 0.5rem;
		background: #EDE9FE;
		color: #6D28D9;
		padding: 0.15rem 0.4rem;
		border-radius: 3px;
	}

	/* Good */
	.ba-good-eyebrow {
		font-size: 0.55rem;
		font-weight: 600;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: #346538;
		margin-bottom: 0.5rem;
	}

	.ba-good-title {
		font-size: 1.2rem;
		font-weight: 800;
		letter-spacing: -0.03em;
		line-height: 0.95;
		color: #111111;
		margin-bottom: 0.5rem;
	}

	.ba-good-body {
		font-size: 0.65rem;
		color: #787774;
		line-height: 1.55;
		margin-bottom: 0.6rem;
	}

	.ba-good-cta {
		font-size: 0.65rem;
		font-weight: 600;
		color: #111111;
	}
</style>
