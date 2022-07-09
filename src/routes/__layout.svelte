<script context="module">
	export const load = async ({ url }) => ({ props: { refresh: url } });
</script>

<script lang="ts">
	import { Body } from 'svelte-body';
	import PageTransition from '$lib/pagetransition/PageTransition.svelte';
	import Header from '$lib/header/Header.svelte';
	import Footer from '$lib/footer/Footer.svelte';
	import '../app.css';

	let isMenuOpen: boolean = false;
	$: mobileMenuOpen = isMenuOpen ? 'mobile-menu-open' : '';
	const handleMenuButtonClick = () => {
		isMenuOpen = !isMenuOpen;
	};

	const handlePageClick = () => {
		if (isMenuOpen) isMenuOpen = !isMenuOpen;
	};

	export let refresh;
</script>

<Body class={mobileMenuOpen} />

<div class="shadow" class:open={isMenuOpen} />
<Header {handleMenuButtonClick} />
<div class="page" class:mobile-menu-open={isMenuOpen} on:click={handlePageClick}>
	<main class:overflow-x-hidden={refresh}>
		<PageTransition {refresh}>
			<slot />
		</PageTransition>
	</main>

	<Footer />
</div>

<style>
	.page {
		display: flex;
		flex-direction: column;
		flex-grow: 1;
		z-index: 20;
		width: 100%;
		height: 100%;
		margin: 0;
		transition: all 0.3s ease-in;
		transform-origin: left center;
		overflow-y: auto;
		overflow-x: hidden;
	}

	.page main {
		flex-grow: 1;
	}

	.mobile-menu-open.page {
		transform: translate(-250px, 100px);
	}

	.shadow {
		z-index: -1;
		position: absolute;
		height: 100vh;
		width: 100vw;
		box-shadow: 3px;
		background: var(--pure-white);
		transform-origin: left center;
		transition: all 0.3s ease-in;
	}

	.shadow.open {
		transform: translate(-250px, 100px);
		border-radius: 10px;
	}
</style>
