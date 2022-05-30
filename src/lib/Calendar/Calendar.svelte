<script>
	import { onMount } from 'svelte'; //Need to use this in order to reference 'document'
	import { each } from 'svelte/internal'; //Using this to loop through the days we have. 
	import Icon from 'svelte-awesome'; 
	import chevronLeft from 'svelte-awesome/icons/chevronLeft'; 
	import chevronRight from 'svelte-awesome/icons/chevronRight';

	//Going to be creating a dynamic way of getting dates to populate the calendar.
	const date = new Date();

	//getMonth will give us a number. Can use that number to access
	//the proper month in an object of months.
	const months = [
		'January',
		'February',
		'March',
		'April',
		'May',
		'June',
		'July',
		'August',
		'September',
		'Ocotber',
		'November',
		'December'
	];

	let days = '';
	onMount(() => {
		document.querySelector('.current-date h1').innerHTML = months[date.getMonth()];
		document.querySelector('.current-date p').innerHTML = date.toDateString();
	});

	/*This gives me the last day of the current month.*/
	const lastDay = new Date(date.getFullYear(), date.getMonth() + 1, 0);
	console.log("This is the last day in May: ", lastDay);
	//let x = 0; 
	//$: x; 
	//$: console.log("This is the value in x:", x); 
</script>

<section class="container">
	<div class="calendar">
		<div class="month">
			<!--<span class="left arrow" />-->
			<Icon data={chevronLeft}/>
			<div class="current-date">
				<h1 />
				<p />
			</div>
			<!--<span class="right arrow" />-->
			<Icon data={chevronRight} /> 
		</div>
		<div class="labels">
			<div>Sun</div>
			<div>Mon</div>
			<div>Tue</div>
			<div>Wed</div>
			<div>Thur</div>
			<div>Fri</div>
			<div>Sat</div>
		</div>
		<div class="days">
			{#each {length: 42} as counter, i}
				<div class="days-inner">
					<p>{++i}</p>
				</div>
			{/each}
        </div>
	</div>
</section>

<style>
	.container{
		justify-content: center;
		align-items: center;
		max-width: 100%;
	}
	.month {
		max-width: 100%;
		height: 12rem;
		background-color: orange;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 0 2rem;
		text-align: center;
		text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
	}
	.month h1 {
		font-size: 3rem;
		font-weight: normal;
		text-transform: uppercase;
		letter-spacing: 0.2rem;
		margin-bottom: 1rem;
	}

	.month p {
		font-size: 1.6rem;
	}
	.labels {
		max-width: 100%;
		height: 5rem;
		padding: 0 0.4rem;
		display: grid;
		grid-auto-flow: row;
		grid-template-columns: repeat(7, 1fr);
		align-items: center;
		justify-content: center;
	}
	.labels div {
		font-size: 1.5rem;
		font-weight: lighter;
		letter-spacing: 0.1rem;
		justify-content: center;
		align-items: center;
		text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
		text-align: center;
	}
	.days {
		max-width: 100%;
		display: grid;
		grid-auto-flow: row;
		grid-template-columns: repeat(7, 1fr);
		justify-content: center;
	}

	.days-inner p{
		text-align: center;
	}

	/*Mobile Layout*/
</style>

