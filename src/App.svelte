<script>
	import Feat from "./Feat.svelte";

	let installUrl;
	let version;

	let promise = getScriptInfo();

	async function getScriptInfo() {
		let response = await fetch(`https://vyneer.me/tools/script`);
		if (response.ok) {
			let data = await response.json();
			installUrl = data['link'];
			version = data['version'];
			return response.ok;
		} else {
			version = "error";
			throw new Error(response.status);
		}
	}
</script>

<main>
	<h1>d.gg utilities</h1>

	{#await promise}
		<h2>Getting script version...</h2>
	{:then}
		{#if version != "error"}
			<h2><a href="{installUrl}" target="_blank">Install version {version}</a></h2>
		{/if}
	{:catch error}
		<h2>HTTP error: {error}</h2>
	{/await}

	<div id="features">
		<Feat title="See what chat's watching!" src="/utilities/images/embeds.png" alt="Screenshot showing a list of top 5 embeds."></Feat>
		<Feat title="Get alerted if your message has ban phrases!" src="/utilities/images/phrases.png" alt="Screenshot showing a red textbox with a banned phrase."></Feat>
		<Feat title="See nukes and mutelinks mode!" src="/utilities/images/nukes.png" alt="Screenshot showing a nuke icon and a mutelinks icon."></Feat>
	</div>
	
	<div id="install">
		<span id="install-text">
			<h3>How to install (<a href="https://streamable.com/y4kanc" target="_blank">NOW IN VIDEO FORM</a>):</h3>
			1. Install <a href="https://www.tampermonkey.net/">Tampermonkey</a> or <a href="https://violentmonkey.github.io/get-it/">Violentmonkey</a> <br>
			2. Copy the installation link <br>
			3. Open the Tampermonkey/Violentmonkey settings <br>
			4a. Tampermonkey: Open the "Utilities" tab, paste the URL inside the textbox and click Install <br>
			4b. Violentmonkey: Click the plus icon, select "Install from URL", paste the URL and click OK <br>
			5. You're done! <br>
		</span>	
	</div>
</main>

<style>
	:global(body) {
		background-color: #333333;
	}

	h1 {
		margin: auto;
		color: white;
		font-size: 3em;
		text-align: center;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
	}

	h2 {
		margin: auto;
		color: white;
		font-size: 2em;
		text-align: center;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
	}

	h3 {
		margin: auto;
		color: white;
		font-size: 1.2em;
		text-align: center;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
	}

	main {
		display: grid;
		flex: 1 0 auto;
		text-align: center;
		padding: 40px;
		max-width: 1020px;
		margin: 0 auto;
		justify-content: center;
		flex-wrap: wrap;
	}

	#features {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
		align-content: space-around;
	}

	#install {
		display: flex;
		align-content: center;
		justify-content: center;
	}

	#install-text {
		align-self: center;
	}

	span {
		color: white;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
	}
</style>