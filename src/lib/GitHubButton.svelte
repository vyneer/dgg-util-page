<script lang="ts">
	let element

	import { onMount } from "svelte";
	import { render as ghRender, GitHubButtonProps } from 'github-buttons';

	const options: GitHubButtonProps = {
	  href: "https://github.com/vyneer/dgg-chat-gui-scripts",
	  title: "Contribute",
	  "data-text": "Contribute",
	  "data-color-scheme": "no-preference: dark; light: light; dark: dark;",
      "data-size": "large",
      "aria-label": "Contribute to vyneer/dgg-chat-gui-scripts on GitHub",
  	}

	onMount(() => {
		ghRender(options, (el) => {
			element.appendChild(el)
		})
	})
</script>

<style>
	div {
		float: right;
	}
</style>

<div bind:this={element}></div>