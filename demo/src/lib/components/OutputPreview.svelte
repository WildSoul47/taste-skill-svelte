<script lang="ts">
	import { onMount } from 'svelte';

	let progress = $state(0);
	let phase = $state(0);
	const phases = [
		{ label: 'Parsing request', icon: '1' },
		{ label: 'Generating code', icon: '2' },
		{ label: 'Cross-checking', icon: '3' }
	];

	onMount(() => {
		const interval = setInterval(() => {
			progress = (progress + 1) % 100;
			if (progress < 33) phase = 0;
			else if (progress < 66) phase = 1;
			else phase = 2;
		}, 80);
		return () => clearInterval(interval);
	});
</script>

<div class="builder">
	{#each phases as p, i}
		<div class="step" class:active={phase === i} class:done={phase > i}>
			<div class="step-indicator">
				{#if phase > i}
					<span class="step-check">&check;</span>
				{:else}
					<span class="step-num">{p.icon}</span>
				{/if}
			</div>
			<div class="step-content">
				<div class="step-label">{p.label}</div>
				{#if phase === i}
					<div class="step-bar">
						<div class="step-fill" style="width: {phase === 0 ? progress * 3 : phase === 1 ? (progress - 33) * 3 : (progress - 66) * 3}%;"></div>
					</div>
				{:else if phase > i}
					<span class="step-done-text">Complete</span>
				{/if}
			</div>
		</div>
	{/each}
	<div class="builder-footer">
		<span class="builder-stat">{progress}%</span>
		<span class="builder-stat-label">delivered</span>
	</div>
</div>

<style>
	.builder {
		border: 1px solid var(--color-border);
		border-radius: var(--radius-md);
		padding: 1rem 1.25rem;
		background: var(--color-surface);
		display: flex;
		flex-direction: column;
		gap: 0.75rem;
	}

	.step {
		display: flex;
		gap: 0.75rem;
		align-items: flex-start;
		opacity: 0.35;
		transition: opacity 0.3s ease;
	}

	.step.active, .step.done {
		opacity: 1;
	}

	.step-indicator {
		width: 22px;
		height: 22px;
		border-radius: 50%;
		border: 1.5px solid var(--color-border);
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
		transition: border-color 0.3s ease, background 0.3s ease;
	}

	.step.active .step-indicator {
		border-color: var(--color-accent);
		background: rgba(37, 99, 235, 0.08);
	}

	.step.done .step-indicator {
		border-color: #346538;
		background: #346538;
	}

	.step-num {
		font-size: 0.6rem;
		font-weight: 700;
		color: var(--color-text-muted);
	}

	.step.active .step-num {
		color: var(--color-accent);
	}

	.step-check {
		font-size: 0.7rem;
		color: white;
		font-weight: 700;
	}

	.step-content {
		flex: 1;
		min-width: 0;
	}

	.step-label {
		font-size: 0.75rem;
		font-weight: 500;
		color: var(--color-text);
		margin-bottom: 0.35rem;
	}

	.step-bar {
		height: 3px;
		background: var(--color-border);
		border-radius: 2px;
		overflow: hidden;
	}

	.step-fill {
		height: 100%;
		background: var(--color-accent);
		border-radius: 2px;
		transition: width 0.1s linear;
	}

	.step-done-text {
		font-size: 0.6rem;
		color: #346538;
		font-weight: 500;
	}

	.builder-footer {
		display: flex;
		align-items: baseline;
		gap: 0.4rem;
		padding-top: 0.5rem;
		border-top: 1px solid var(--color-border);
	}

	.builder-stat {
		font-size: 1.5rem;
		font-weight: 800;
		letter-spacing: -0.03em;
		color: var(--color-text);
		line-height: 1;
		font-variant-numeric: tabular-nums;
	}

	.builder-stat-label {
		font-size: 0.6rem;
		color: var(--color-text-muted);
		text-transform: uppercase;
		letter-spacing: 0.08em;
	}
</style>
