<script lang="ts">
	let hovered = $state<number | null>(null);
</script>

<div class="card">
	<div class="card-header">
		<span class="card-eyebrow">Project Board</span>
		<span class="card-count">3 tasks</span>
	</div>
	<div class="card-list">
		{#each ['Design system tokens', 'Component audit', 'Spacing scale'] as task, i}
			<button
				class="card-item"
				class:hovered={hovered === i}
				onmouseenter={() => hovered = i}
				onmouseleave={() => hovered = null}
			>
				<span class="item-check" class:done={i === 0}></span>
				<span class="item-text" class:completed={i === 0}>{task}</span>
				<span class="item-tag" style="background: {['#E1F3FE', '#EDF3EC', '#FBF3DB'][i]}; color: {['#1F6C9F', '#346538', '#956400'][i]};">{['Design', 'QA', 'Dev'][i]}</span>
			</button>
		{/each}
	</div>
	<div class="card-progress">
		<div class="progress-track">
			<div class="progress-fill"></div>
		</div>
		<span class="progress-label">1 of 3 complete</span>
	</div>
</div>

<style>
	.card {
		background: #F9F9F8;
		border: 1px solid #EAEAEA;
		border-radius: 10px;
		padding: 1rem 1.25rem;
		font-family: var(--font-display);
	}

	.card-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 0.75rem;
	}

	.card-eyebrow {
		font-size: 0.85rem;
		font-weight: 600;
		color: #111111;
		letter-spacing: -0.01em;
	}

	.card-count {
		font-size: 0.6rem;
		color: #787774;
		letter-spacing: 0.03em;
	}

	.card-list {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
		margin-bottom: 0.75rem;
	}

	.card-item {
		display: flex;
		align-items: center;
		gap: 0.6rem;
		padding: 0.5rem 0.6rem;
		border-radius: 6px;
		border: none;
		background: transparent;
		cursor: pointer;
		font-family: inherit;
		transition: background 0.15s ease;
		width: 100%;
		text-align: left;
	}

	.card-item.hovered {
		background: #F0F0EE;
	}

	.item-check {
		width: 14px;
		height: 14px;
		border-radius: 4px;
		border: 1.5px solid #D0D0CE;
		flex-shrink: 0;
		position: relative;
	}

	.item-check.done {
		background: #346538;
		border-color: #346538;
	}

	.item-check.done::after {
		content: '';
		position: absolute;
		left: 3.5px;
		top: 1px;
		width: 4px;
		height: 8px;
		border: solid white;
		border-width: 0 1.5px 1.5px 0;
		transform: rotate(45deg);
	}

	.item-text {
		font-size: 0.75rem;
		color: #2F3437;
		flex: 1;
	}

	.item-text.completed {
		text-decoration: line-through;
		color: #787774;
	}

	.item-tag {
		font-size: 0.5rem;
		font-weight: 500;
		padding: 0.15rem 0.45rem;
		border-radius: 3px;
		letter-spacing: 0.02em;
	}

	.card-progress {
		display: flex;
		align-items: center;
		gap: 0.6rem;
	}

	.progress-track {
		flex: 1;
		height: 3px;
		background: #EAEAEA;
		border-radius: 2px;
		overflow: hidden;
	}

	.progress-fill {
		width: 33%;
		height: 100%;
		background: #346538;
		border-radius: 2px;
		animation: progress-grow 2s ease-in-out infinite alternate;
	}

	@keyframes progress-grow {
		0% { width: 33%; }
		100% { width: 40%; }
	}

	.progress-label {
		font-size: 0.55rem;
		color: #787774;
		white-space: nowrap;
	}
</style>
