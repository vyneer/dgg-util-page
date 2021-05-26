<script>
	export let title;
	export let src;
	export let alt;
</script>

<style>
	h2 {
		margin: auto;
		color: white;
		font-size: 1.2em;
		text-align: center;
		font-family: "Roboto",Helvetica,"Trebuchet MS",Verdana,sans-serif;
	}

	img {
		width: 275px;
	}

	.feature {
		display: block;
		justify-content: space-between;
		text-align: center;
		width: 300px;
	}
</style>

<div class="feature">
	<h2>{title}</h2>
	<img {src} {alt}>
</div>