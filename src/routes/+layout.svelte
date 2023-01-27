<script>
	import '@fontsource/poppins'; // The font we are gonna serve with fontsource
</script>

<slot />

<style>
	/* using :global because of Svelte */
	:global(body) {
		font-family: 'Poppins', sans-serif;
	}
</style>
