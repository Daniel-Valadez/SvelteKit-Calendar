<script>
	import { onMount } from 'svelte'; //Need to use this in order to reference 'document'

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
	//let monthDays = "";

	onMount(() => {
		document.querySelector('.current-date h1').innerHTML = months[date.getMonth()];
		document.querySelector('.current-date p').innerHTML = date.toDateString();
		const monthDays = document.querySelector('.days');
		for (let i = 1; i <= 31; ++i) {
			days += `<div>${i}</div>`;
            //days.classList.add("days-inner"); 
			monthDays.innerHTML = days;
		}
	});
</script>

<section class="container">
	<div class="calendar">
		<div class="month">
			<span class="left arrow" />
			<div class="current-date">
				<h1 />
				<p />
			</div>
			<span class="right arrow" />
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
        </div>
	</div>
</section>

<style>
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
		width: 100%;
		height: 5rem;
		padding: 0 0.4rem;
		display: flex;
		align-items: center;
	}
	.labels div {
		font-size: 1.5rem;
		font-weight: lighter;
		letter-spacing: 0.1rem;
		width: calc(44.2rem / 7);
		display: flex;
		justify-content: center;
		align-items: center;
		text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
	}
	.days {
		/*width: 100%;
		display: flex;
		flex-wrap: wrap;
		padding: 0.2rem;*/
        font-size: 1.4rem;
		margin: 0.3rem;
		width: calc(40.2rem / 7);
		height: 5rem;
		display: flex;
        flex-wrap: wrap;
		text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
		transition: background-color 0.2s;
	}
</style>
