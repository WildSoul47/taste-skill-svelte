<script lang="ts">
	let { children } = $props();
</script>

{@render children()}

<style>
	:global(*) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(:root) {
		--color-canvas: #F7F6F3;
		--color-surface: #FFFFFF;
		--color-text: #1A1A1A;
		--color-text-muted: #6B6B6B;
		--color-border: rgba(0, 0, 0, 0.07);
		--color-accent: #2D5A27;
		--font-display: 'Outfit', system-ui, sans-serif;
		--font-serif: 'Instrument Serif', Georgia, serif;
		--radius-sm: 6px;
		--radius-md: 10px;
		--radius-lg: 14px;
		--radius-xl: 18px;
		--shadow-diffuse: 0 12px 32px -8px rgba(0, 0, 0, 0.06);
		--ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
	}

	:global(body) {
		font-family: var(--font-display);
		background: var(--color-canvas);
		color: var(--color-text);
		line-height: 1.6;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	:global(a) {
		color: inherit;
		text-decoration: none;
	}

	:global(img) {
		display: block;
		max-width: 100%;
	}

	:global(::selection) {
		background: rgba(45, 90, 39, 0.12);
	}
</style>
