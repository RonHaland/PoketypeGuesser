<script>
	import TypeGrid from "./TypeGrid.svelte";
</script>

<svelte:head>
	<title>PokeTypes</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		Pokemon Type Effectiveness Guesser
	</h1>

	<div class="grid">
		<TypeGrid />
	</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.grid {
		display: flex;
		flex-direction: row;
		justify-content: center;
	}
</style>
