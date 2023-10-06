<script>
	import Header from './Header.svelte';
    import Spline from './Spline.svelte';
	import './styles.css';
</script>

<div class="app">
	<Header />
	<main>
		<slot />
		<Spline/>
	</main>
	<footer>
		<p>visit <a href="https://app.spline.design/community/file/33c3e7b7-b30c-4755-acd7-7fda980f4f67">SplineCommunity</a> for scene</p>
		<p>visit <a href="https://github.com/executionreverted/svelte-spline-particle-fx">github</a> for source code</p>
		<p>visit <a href="https://kit.svelte">kit.svelte.dev</a> to learn SvelteKit</p>
		<p>visit <a class="spline" href="https://spline.design">spline.design</a> to learn about Spline</p>
	</footer>
</div>

<style>
	.spline{
		color: rgb(63, 145, 145);
	}
	.app {
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
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
