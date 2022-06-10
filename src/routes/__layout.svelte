<script>
	import Navbar from '$lib/Navbar/Navbar.svelte';
	import '../app.css';
</script>

<Navbar />

<main>
	<slot />
</main>

<footer>
	<p>
		<a target="_blank" href="https://icons8.com/icon/12776/calendar">Calendar</a> icon by
		<a target="_blank" href="https://icons8.com">Icons8</a>
	</p>
</footer>

<style>
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		/*padding: 1rem;*/
		width: 100%;
		/*max-width: 1024px;*/
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	/*footer a {
		font-weight: bold;
	}*/

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
