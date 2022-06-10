<!--The brackets over the name will allow this page to
pool dynamic data.-->
<script>
	//Need to parse the URL to find out what the day is.
	import { page } from '$app/stores';
	let date = $page.url.pathname.replace('/day/', '');
	date = date.replaceAll('%20', ' '); 
	//console.log(day);
	let weather = '70 Degrees';
	import plusCircle from 'svelte-awesome/icons/plusCircle';
	import { Icon } from 'svelte-awesome';
	import { onMount } from 'svelte/internal';
	import TodoApi from '../../TodoApi';
	import { items } from '../../strores';
	import Item from '$lib/Item/Item.svelte';
	import NewItem from '$lib/NewItem/NewItem.svelte';
	let number = 0; 
	function handleNewItem({ detail: text }) {
		$items = [
			{
				id: ++number,
				text,
				complete: false
			},
			...$items
		];
		TodoApi.save($items);
	}
	function handleUpdate({ detail }) {
		const index = $items.findIndex((item) => item.id === detail.id);
		$items[index] = detail;
		TodoApi.save($items);
	}
	function handleDelete({ detail: id }) {
		$items = $items.filter((item) => item.id !== id);
		TodoApi.save($items);
	}

	//Function to sort the items on the list. 
	let itemsSorted = [];
	$: {
		itemsSorted = [...$items];
		itemsSorted.sort((a, b) => {
			if (a.complete && b.complete) return 0;
			if (a.complete) return 1;
			if (b.complete) return -1;
		});
	}

	//Fecth items pre-existing on loading.
	onMount(async () => {
		$items = await TodoApi.getAll();
	});
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
	<div class="list">
		<NewItem on:newitem={handleNewItem} />
		{#each itemsSorted as item (item)}
			<Item {...item} on:update={handleUpdate} on:delete={handleDelete} />
		{:else}
			<p class="list-status">No Items Exist</p>
		{/each}
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
	.list {
		padding: 15px;
	}
	.list-status {
		margin: 0;
		text-align: center;
		color: #ffffff;
		font-weight: bold;
		font-size: 1.1em;
	}
</style>
