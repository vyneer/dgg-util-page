<script lang="ts">
  import Fa from 'svelte-fa'
  import { faHome } from '@fortawesome/free-solid-svg-icons'

  import Feat from "./lib/Feat.svelte";
  import GHButton from "./lib/GitHubButton.svelte"

  import embedsImg from "./assets/embeds.png";
  import nukesImg from "./assets/nukes.png";
  import phrasesImg from "./assets/phrases.png";

  let installUrl;
  let version;
  let installUrlDev;
  let versionDev;

  let promise = getScriptInfo(false);
  let promiseDev = getScriptInfo(true);

  async function getScriptInfo(dev) {
    let url = dev
      ? "https://vyneer.me/tools/script/dev"
      : "https://vyneer.me/tools/script";
    let response = await fetch(url);
    if (response.ok) {
      let data = await response.json();
      if (dev) {
        installUrlDev = data["link"];
        versionDev = data["version"];
      } else {
        installUrl = data["link"];
        version = data["version"];
      }
      return response.ok;
    } else {
      if (dev) {
        versionDev = "error";
      } else {
        version = "error";
      }
      throw new Error(`${response.status}`);
    }
  }
</script>

<header>
  <a class="home-button" href="https://vyneer.me"><Fa icon={faHome} /></a>
</header>

<main>
  <h1>d.gg utilities</h1>

  {#await promise}
    <h2>Getting script version...</h2>
  {:then}
    {#if version != "error"}
      <h2>
        <a href={installUrl} target="_blank">Install version {version}</a>
      </h2>
    {/if}
  {:catch error}
    <h2>HTTP error: {error}</h2>
  {/await}

  <div id="features">
    <Feat
      title="See what chat's watching!"
      src={embedsImg}
      alt="Screenshot showing a list of top 5 embeds."
    />
    <Feat
      title="Get alerted if your message has ban phrases!"
      src={phrasesImg}
      alt="Screenshot showing a red textbox with a banned phrase."
    />
    <Feat
      title="See nukes and mutelinks mode!"
      src={nukesImg}
      alt="Screenshot showing a nuke icon and a mutelinks icon."
    />
  </div>

  <div id="install">
    <span id="install-text">
      <h3>How to install:</h3>
      1. Install <a href="https://www.tampermonkey.net/">Tampermonkey</a>, 
      <a href="https://violentmonkey.github.io/get-it/">Violentmonkey</a> or  
      <a href="https://addons.mozilla.org/en-US/firefox/addon/firemonkey/">FireMonkey (Firefox)</a>
      <br />
      (<a href="https://itunes.apple.com/us/app/userscripts/id1463298887">Userscripts (Safari)</a> is untested, but also seems to work)
      <br />
      2. Click the install link above <br />
      3. Click "Install" or "Confirm installation" or "OK" <br />
      4. You're done! <br />
    </span>
  </div>
</main>

<footer>
  <div style="float: left;">
    {#await promiseDev}
      <span class="small-link">Getting script version...</span>
    {:then}
      {#if versionDev != "error"}
        <a class="small-link" href={installUrlDev} target="_blank"
          >Install beta/dev version {versionDev}</a
        >
      {/if}
    {:catch error}
      <span class="small-link">HTTP error: {error}</span>
    {/await}
  </div>
  <GHButton></GHButton>
</footer>

<style>
  :global(body) {
    background-color: #333333;
  }

  .small-link {
    font-size: 0.8em;
    font-family: "Roboto", Helvetica, "Trebuchet MS", Verdana, sans-serif;
    color: #3a3a3a !important;
  }

  h1 {
    margin: auto;
    color: white;
    font-size: 3em;
    text-align: center;
    font-family: "Roboto", Helvetica, "Trebuchet MS", Verdana, sans-serif;
  }

  h2 {
    margin: auto;
    color: white;
    font-size: 2em;
    text-align: center;
    font-family: "Roboto", Helvetica, "Trebuchet MS", Verdana, sans-serif;
  }

  h3 {
    margin: auto;
    color: white;
    font-size: 1.2em;
    text-align: center;
    font-family: "Roboto", Helvetica, "Trebuchet MS", Verdana, sans-serif;
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
    font-family: "Roboto", Helvetica, "Trebuchet MS", Verdana, sans-serif;
  }
</style>
