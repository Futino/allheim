<script lang="ts">
	import { base } from '$app/paths';
	import Header from '$lib/components/organisms/Header.svelte';
	import Footer from '$lib/components/organisms/Footer.svelte';
	// import Button from '$lib/components/atoms/Button.svelte';
	const months = [
		"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"
	];

	const days = [
		"Sunday", "Monday", "Tuesday", "Wednessday", "Thursday", "Friday", "Saturday"
	]
	

	// Custom
	const numWeeks = 24;
	const weekdays = [3, 5];
	const time = "19:00 - 21:00"



	let weeks: { day: string, month: string, date: number }[][] = [];

	for (let w = 0; w < numWeeks; ++w) {


		let week: { day: string, month: string, date: number }[] = [];

		for (let d = 0; d < weekdays.length; ++d) {
			let curr = new Date();

			let day = new Date(curr.setDate(curr.getDate() - curr.getDay() + weekdays[d] + w * 7))

			week.push({
					day: days[day.getDay()].substring(0, 3),
					month: months[day.getMonth()].substring(0, 3),
					date: day.getDate()
			});
		}

		weeks.push(week);
	}
	console.log(weeks)
</script>

<Header />


<section
	class="py-20 px-4 border-b shadow-2xl sm:px-6 md:px-8 border-primary-light/40 dark:border-primary-dark/40"
>
    <div class="grid justify-items-center space-y-12 mx-auto">
        <h1 class="display-large">Schedule</h1>

        <h2 class="headline-large">Please enter your name and click the sessions you want to join.</h2>

		<input class="bg-primary-light dark:bg-primary-dark p-2 text-center placeholder-primary-on-light/60 dark:placeholder-primary-on-dark/60 text-primary-on-light dark:text-primary-on-dark headline-large" placeholder="Your Name" />
    </div>
</section>

<section class="w-full h-full grid gap-y-5 gap-x-12 lg:grid-cols-2 2xl:grid-cols-3 justify-center place-items-center p-12 xl:px-60 2xl:px-96">
	{#each weeks as week, index (index)}
	<div class="w-full h-full flex flex-row gap-5 p-5 bg-white/5 shadow-lg shadow-black rounded-lg">
		{#each week as { day, month, date }}
		<button class='h-full w-full p-3 shadow-lg rounded-lg text-center bg-secondary-light dark:bg-secondary-dark text-secondary-on-light dark:text-secondary-on-dark'>
			<p class="headline-large">{day}</p>
			<p class='display-large lg:display-medium'>{month}. {date}</p>
			<p class="title-large">{time}</p>
		</button>
		{/each}
	</div>
	{/each}
</section>

<Footer />;