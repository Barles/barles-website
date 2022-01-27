<script lang="ts">
import Buttons from "./examples/Buttons.svelte";
</script>

<main>
	<Buttons />
</main>

<svelte:head>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.22.0/themes/prism.min.css" rel="stylesheet" />
</svelte:head>

<style>
:global(html) {
	background: #333;
}
main {
	margin-top: 15px;
}
</style>