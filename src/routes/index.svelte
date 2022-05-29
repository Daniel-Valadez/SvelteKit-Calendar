<script context="module">
	export const prerender = true;
</script>

<script>
	import Calendar from "$lib/Calendar/Calendar.svelte";
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="SvelteKit calendar app" />
</svelte:head>

<Calendar /> 


