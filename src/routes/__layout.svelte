<script lang="ts">
	import Header from '$lib/header/Header.svelte';
	import Footer from '$lib/footer/Footer.svelte';
	import '../app.css';

	let isMenuOpen: boolean = false;
	$: document.body.classList[isMenuOpen ? 'add' : 'remove']('mobile-menu-open');
	const handleMenuButtonClick = () => { isMenuOpen = !isMenuOpen;}
</script>

<div class="shadow" class:open={isMenuOpen}></div>
<Header {handleMenuButtonClick} />
<div class="page" class:mobile-menu-open={isMenuOpen}>
	
	<main>
		<slot />
	</main>
	
</div>
<Footer />

<style>
	.page {
		flex-grow: 1;
		z-index: 20;
		width:100%;
		margin:0;
		transition: all 0.3s ease-in;
		transform-origin: left center;
	}

	.mobile-menu-open.page {
		transform: scale(.85) translateX(-300px);
	}

	.shadow {
		position:absolute;
		height:100vh;
		width:100vw;
		background: var(--pure-white);
		transform-origin: left center;
		transition: all 0.3s ease-in;
	}

	.shadow.open {
		transform: scale(.85) translateX(-300px);
	}
</style>
