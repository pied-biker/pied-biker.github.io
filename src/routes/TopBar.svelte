<script lang="ts">
    import Menu from 'svelte-material-icons/Menu.svelte';
	import ThemeLightDark from 'svelte-material-icons/ThemeLightDark.svelte';
	import type TopAppBarComponentDev from '@smui/top-app-bar';
	import TopAppBar, { Row, Section, Title, AutoAdjust } from '@smui/top-app-bar';

    import type MenuBar from './MenuBar.svelte';

    let topAppBar: TopAppBarComponentDev;
	export let menu: MenuBar;
	const icon_size = '2em';

    let lightTheme =
		typeof window === 'undefined' || window.matchMedia('(prefers-color-scheme: light)').matches;
	$: modeLabel = `Switch to ${lightTheme ? 'dark' : 'light'} mode`;

	const toggleMode = () => {
		lightTheme = !lightTheme;
		let themeLink: HTMLLinkElement = document.head.querySelector('#theme')!;
		if (!themeLink) {
			themeLink = document.createElement('link');
			themeLink.rel = 'stylesheet';
			themeLink.id = 'theme';
		}
		themeLink.href = `/smui${lightTheme ? '' : '-dark'}.css`;
		document.head
			.querySelector('link[href="/smui-dark.css"]')!
			.insertAdjacentElement('afterend', themeLink);
	};

	function toggleMenubar() {
		menu.openMenu();
	}

</script>

<TopAppBar bind:this={topAppBar} variant="standard" dense>
	<Row>
		<Section>
			<button class="icon-button" on:click={toggleMenubar}>
				<Menu size={icon_size} />
			</button>
			<Title>Pied Biker</Title>
		</Section>
		<Section align="end">
			<button class="icon-button" on:click={toggleMode}>
				<ThemeLightDark size={icon_size} title={modeLabel} />
			</button>
		</Section>
	</Row>
</TopAppBar>
<AutoAdjust {topAppBar}>
	<slot />
</AutoAdjust>


<style>
	.icon-button {
		background-color: transparent;
		border: none;
		outline: none;
		color: inherit;
	}
</style>

