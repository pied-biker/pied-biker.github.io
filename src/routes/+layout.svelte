<script lang="ts">
	import '../app.scss';
	import TopBar from "./TopBar.svelte";
	import MenuBar from './MenuBar.svelte';
	
	let menu: MenuBar;
</script>

<div class="app">
	<TopBar {menu}/>
	<MenuBar bind:this={menu}/>
	<main>
		<slot />
	</main>
</div>

<style>
	.app {
		font-family: 'Roboto', sans-serif;
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>
