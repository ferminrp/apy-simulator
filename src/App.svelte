<script>
	let mode = 'input';
	let capital = 3000;
	let apy = 0.15;
	let final;
	let timer;
	let initial_date;

	function start() {
		initial_date = new Date();
		mode = 'simular'
		final = capital;
		timer = setInterval(function() {
			let now = new Date();
			// miliseconds between initial and now
			let diff = now.getTime() - initial_date.getTime();
			final = capital * Math.pow(1 + apy / 365, diff / (1000 * 60 * 60 * 24));
            }, 10);
	}
</script>

<main>
	{#if mode == 'input'}
	<label for="capital">Capital Inicial</label>
	<input id="capital" type="number" bind:value="{capital}">
	<label for="apy">APY</label>
	<input id="apy" type="number" bind:value="{apy}">
	<button on:click="{start}">Simular</button>
	{:else}
	<p>{final}</p>
	{/if}
</main>