<script>
	let promise = getDoUsername();

	async function getDoUsername() {
		const res = await fetch(`https://thatcopy.pw/do/`);
		const text = await res.text();

		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}

	function handleClick() {
		promise = getDoUsername();
	}
</script>

<main>
	<div id="wrap">
	<button on:click={handleClick}>
		Get a random DigitalOcean username
	</button>

	{#await promise}
		<h1>...loading</h1>
	{:then username}
		<h1>{username}</h1>
	{:catch error}
		<h1 style="color: red">{error.message}</h1>
	{/await}
	<img id="sammy" src="/sammy.webp" alt="Sammy">
</div>
</main>

<style>
	#wrap{
		display: flex;
		width: 30%;
  		margin-left: auto;
  		margin-right: auto;
		justify-content: center;
		flex-direction: column;
	}
	#sammy{
		display: block;
  		margin-left: auto;
  		margin-right: auto;
  		width: 50%;
	}
	h1{
		text-align: center;
	}
	
</style>
