<script>
	let promise = getDoUsername();
	let darkmode = false;

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

	function setDarkMode() {
		const headings = document.getElementsByTagName("h1");
		const buttons = document.getElementsByTagName("button");
		if (!darkmode) {
			darkmode = true;
			document.body.style.background = '#2E2C2F';
			for (let heading of headings) {
				if (heading.id != "error") heading.style.color = 'white';
			}
			for (let button of buttons) {
    			if (button.id == "darkmode") {
					button.innerHTML = "Darkmode: On";
				}
				button.style.background = '#475B63';
				button.style.color = 'white';
			}
		} else {
			darkmode = false;
			document.body.style.background = 'white';
			for (let heading of headings) {
				if (heading.id != "error") heading.style.color = 'black';
			}
			for (let button of buttons) {
				if (button.id == "darkmode") {
					button.innerHTML = "Darkmode: Off";
				}
				button.style.background = '#f4f4f4';
				button.style.color = 'black';
			}
		}
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
		<h1 id="error" style="color: red">{error.message}</h1>
	{/await}
	<img id="sammy" src="/sammy.webp" alt="Sammy">
	<button id="darkmode" on:click={setDarkMode}>
		Darkmode: Off
	</button>
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
		margin-bottom: 24px;
	}
	h1{
		text-align: center;
	}
	
</style>
