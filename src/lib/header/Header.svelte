<script lang="ts">
	export let handleMenuButtonClick: svelte.JSX.MouseEventHandler<HTMLButtonElement>;
</script>

<header class="test">
	<a class="logo" href="">logo</a>

	<button class="menu-toggle" on:click={handleMenuButtonClick}>
		<span class="line"></span>
	</button>

	<ul class="nav-links">
		<li><a href="/">home</a></li>
		<li><a href="/about">about</a></li>
		<li><a href="/gallery">gallery</a></li>
		<li><a href="/contact">contact</a></li>
	</ul>
</header>

<style>
    header {
		position: relative;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
        width:100%;
		max-width: 1280px;
		margin: 0 auto;
		height: 60px;
        background: none;
    }

	.logo {
		padding: 10px 20px;
	}

	.menu-toggle {
		position: relative;
		border: transparent;
		background: none;
		height: 60px;
		width: 60px;
		cursor: pointer;
	}

	.menu-toggle .line {
		display:block;
		position: absolute;
		box-sizing: border-box;
		z-index:30;
		height:25px;
		width:30px;
		top: 17px;
		left: 17px;
		border-top:2px solid var(--accent-color);
		transition: all 0.3s ease-in
	}
	.menu-toggle .line::before {
		content: "";
		display:block;
		position:absolute;
		height:2px;
		width:30px;
		top: 10px;
		left: 0;
		background: var(--accent-color);
		transition: all 0.3s ease-in
	}
	.menu-toggle .line::after {
		content: "";
		display:block;
		position:absolute;
		height:2px;
		width:30px;
		bottom: 0;
		left: 0;
		background: var(--accent-color);
		transition: all 0.3s ease-in
	}


	.mobile-menu-open * .menu-toggle {
		position: sticky;
		top:0;
		right:0;
	}

	.mobile-menu-open * .menu-toggle .line {
		border-color: transparent;
	}
	.mobile-menu-open * .menu-toggle .line::before {
		transform: rotate(45deg);
		width: 33px;
		left: -2px;
	}
	.mobile-menu-open * .menu-toggle .line::after {
		transform: rotate(135deg);
		width: 33px;
		bottom: 11px;
		left: -2px;
	}

	.nav-links {
		position: absolute;
		display: flex;
		flex-direction: column;
		list-style: none;
		width:200px;
		height: 100%;
		top: 60px;
		right:-200px;
		transition: all 0.3s ease-in;
	}
	.mobile-menu-open * .nav-links {
		transform: translate(-200px);
	}

	.nav-links li {
		padding: 10px 30px;
	}

	@media (min-width: 640px) {
		.nav-links {
			position: relative;
			flex-direction: row;
			top:auto;
			right:auto;
			width:auto;
			height:auto;
		}

		.nav-links li a {
			padding: 10px 20px;
		}
		.menu-toggle {
			display: none;
		}
	}
</style>
