<script>
	import { onMount } from 'svelte'; //Need to use this in order to reference 'document'
	import { each } from 'svelte/internal'; //Using this to loop through the days we have.
	import Icon from 'svelte-awesome';
	import chevronLeft from 'svelte-awesome/icons/chevronLeft';
	import chevronRight from 'svelte-awesome/icons/chevronRight';

	//Going to be creating a dynamic way of getting dates to populate the calendar.
	const date = new Date();
	let month = '';
	let currentDate = '';
	let prevNumbers = []; //an array of dates of the previous month to render
	let numbers = []; //The current months numbers to render.
	let nextNumbers = []; //The next months numbers to render;
	//let totalLength = 0;
	//let totalArray = [];
	let renderCalendar = () => {
		prevNumbers = [];
		numbers = [];
		nextNumbers = [];
		//totalArray = []

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
		date.setDate(1);
		month = months[date.getMonth()];
		//console.log('The month is: ', month);
		currentDate = new Date().toDateString();

		const lastDay = new Date(date.getFullYear(), date.getMonth() + 1, 0).getDate();
		const firstDay = date.getDay();
		const prevLast = new Date(date.getFullYear(), date.getMonth(), 0).getDate();
		const lastDayIndex = new Date(date.getFullYear(), date.getMonth() + 1, 0).getDay();
		const nextDays = 7 - lastDayIndex - 1;

		for (let x = firstDay; x > 0; --x) {
			prevNumbers.push(prevLast - x + 1);
		}
		//console.log('The array of previous numbers: ', prevNumbers);

		for (let i = 1; i <= lastDay; ++i) {
			numbers.push(i);
		}

		//console.log('The array of numbers to render this month....', numbers);

		for (let j = 1; j <= nextDays; ++j) {
			nextNumbers.push(j);
		}

		//console.log('The array of numbers to be pushed the next month, ', nextNumbers);
		//totalLength = prevNumbers.length + numbers.length + nextNumbers.length;
		//totalArray = prevNumbers.concat(numbers, nextNumbers);
		//console.log('Total array', totalArray);
	};

	/*Single on-click handler*/
	let shiftCalendar = (offset) => {
		date.setMonth(date.getMonth() + offset);
		renderCalendar();
	};

	/*The first call provides the initial values for the calendar.*/
	renderCalendar();
</script>

<section class="container">
	<div class="calendar">
		<div class="month">
			<span on:click={() => shiftCalendar(-1)}>
				<Icon data={chevronLeft} scale={2} style="cursor: pointer;" />
			</span>
			<div class="current-date">
				<h1>{month}</h1>
				<p>{currentDate}</p>
			</div>
			<span on:click={() => shiftCalendar(1)}>
				<Icon data={chevronRight} scale={2} style="cursor: pointer;" />
			</span>
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
			{#each { length: prevNumbers.length } as counter, i}
				<div class="other-days days-inner">
					<p>{prevNumbers[i]}</p>
				</div>
			{/each}
			{#each { length: numbers.length } as counter, i}
				<a href={"/day/" + (i + 1)}>
					<div class="days-inner">
						<p>{numbers[i]}</p>
					</div>
				</a>
			{/each}
			{#each { length: nextNumbers.length } as counter, i}
				<div class="other-days days-inner">
					<p>{nextNumbers[i]}</p>
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	.container {
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
		text-align: center;
		row-gap: 5rem;
	}

	.other-days p{
		opacity: 0.5;
	}

	.days-inner{
		border: solid 0.1rem black;  
	}
	.days-inner p {
		font-weight: bold;
		place-self: center;
	}
	a:hover{
		text-decoration: none;
		background-color: orange;
	}

	/*Mobile Layout*/
	
</style>
