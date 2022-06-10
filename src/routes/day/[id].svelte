<!--The brackets over the name will allow this page to
pool dynamic data.-->
<script>
	//Need to parse the URL to find out what the day is.
	import { page } from '$app/stores';
	const date = $page.url.pathname.replace('/day/', '');
	//console.log(day);
	let weather = '70 Degrees';
	import plusCircle from 'svelte-awesome/icons/plusCircle';
	import { Icon } from 'svelte-awesome';
</script>

<section>
	<div class="parent-box">
		<div class="left-box">
			<p>{date}</p>
			{#if weather}
				<p>{weather}</p>
			{/if}
		</div>
		<div class="right-box">
			<p class="add-elements">Create Event</p>
			<Icon data={plusCircle} scale={1.5} style="cursor: pointer; color: orangered;" />
		</div>
	</div>
</section>

<style>
	.parent-box {
		display: grid;
		width: 100%;
		justify-content: space-around;
		grid-auto-flow: column;
	}
	p {
		font-size: 1.5rem;
		font-weight: bold;
	}

	.right-box,
	.left-box {
		display: flex;
		place-items: center;
		gap: 1rem;
	}
</style>
