<script>
	import Feat from "./Feat.svelte";

	let installUrl;
	let version;
	let installUrlDev;
	let versionDev;

	let promise = getScriptInfo(false);
	let promiseDev = getScriptInfo(true);

	async function getScriptInfo(dev) {
		let url = dev ? "https://vyneer.me/tools/script/dev" : "https://vyneer.me/tools/script";
		let response = await fetch(url);
		if (response.ok) {
			let data = await response.json();
			if (dev) {
				installUrlDev = data['link'];
				versionDev = data['version'];
			} else {
				installUrl = data['link'];
				version = data['version'];
			}
			return response.ok;
		} else {
			if (dev) {
				versionDev = "error";
			} else {
				version = "error";
			}
			throw new Error(response.status);
		}
	}
</script>

<header>
	<a href="https://vyneer.me"><i class="home-button fas fa-home"></i></a>
</header>

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
			<h3>How to install:</h3>
			1. Install <a href="https://www.tampermonkey.net/">Tampermonkey</a> or <a href="https://violentmonkey.github.io/get-it/">Violentmonkey</a> <br>
			2. Click the install link above <br>
			3. Click "Install"/"Confirm installation" <br>
			4. You're done! <br>
		</span>	
	</div>
</main>

<footer>
	<div style="float: left;">
		{#await promiseDev}
			<h2>Getting script version...</h2>
		{:then}
			{#if versionDev != "error"}
				<a class="small-link" href="{installUrlDev}" target="_blank">Install beta/dev version {versionDev}</a>
			{/if}
		{:catch error}
			<h2>HTTP error: {error}</h2>
		{/await}
	</div>
	<div style="float: right;">
		<a class="github-button" href="https://github.com/vyneer/dgg-chat-gui-scripts" data-color-scheme="no-preference: dark; light: light; dark: dark;" data-size="large" aria-label="Contribute to vyneer/dgg-chat-gui-scripts on GitHub">Contribute</a>
	</div>
</footer>

<style>
	:global(body) {
		background-color: #333333;
	}

	.small-link {
		font-size: 0.8em;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
		color: #3a3a3a !important;
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

	.home-button {
		color: white;
		font-size: xx-large;
	}

	span {
		color: white;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
	}
</style>