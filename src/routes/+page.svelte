<script>
	import {
		recommendations,
		star1,
		star2,
		star3,
		formSubmitted,
		loading,
		language
	} from '../stores/store';
	import { translations } from '../utils/translation';
	import { goto } from '$app/navigation';
	import Spinner from '../spinner/spinner.svelte';
	import SpinnerMalay from '../spinner/spinner-malay.svelte';
	import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';

	let currentLanguage;

	language.subscribe((value) => {
		currentLanguage = value;
	});

	export async function addToRecommendations(evt) {
		loading.set(true);

		const reviewData = {
			recommendation: evt.target['recommendation'].value
		};

		const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/new-bad-review', {
			method: 'POST',
			mode: 'cors',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(reviewData)
		});

		loading.set(false);
		formSubmitted.set(true);
	}

	function clickStar1() {
		star2.set(false);
		star3.set(false);
		star1.set(true);
		document.querySelector('.recommendation-form').classList.remove('hidden');
	}

	function clickStar2() {
		star3.set(false);
		star1.set(true);
		star2.set(true);
		document.querySelector('.recommendation-form').classList.remove('hidden');
	}

	function clickStar3() {
		star1.set(true);
		star2.set(true);
		star3.set(true);
		document.querySelector('.recommendation-form').classList.remove('hidden');
	}

	function clickStar4() {
		window.location.href =
			'https://www.google.com/search?si=ACC90nwjPmqJHrCEt6ewASzksVFQDX8zco_7MgBaIawvaF4-7vzIn6vo1I14Od8RALYKInQ_rzwmzZrHhYtJZ8mU5yNZPQPEAd6QIXtT5YtzhQZPxDKWZFuPQGMRCu2oY5bbz51b6AJYvoqY4NOHCtUzcDL4Z1b8YA%3D%3D&hl=en-MY&q=poliklinik+utama+port+dickson+reviews&kgs=0e755424154859a1&shndl=30&shem=ssim&source=sh/x/loc/osrp/m5/3';
	}

	function clickStar5() {
		window.location.href =
			'https://www.google.com/search?si=ACC90nwjPmqJHrCEt6ewASzksVFQDX8zco_7MgBaIawvaF4-7vzIn6vo1I14Od8RALYKInQ_rzwmzZrHhYtJZ8mU5yNZPQPEAd6QIXtT5YtzhQZPxDKWZFuPQGMRCu2oY5bbz51b6AJYvoqY4NOHCtUzcDL4Z1b8YA%3D%3D&hl=en-MY&q=poliklinik+utama+port+dickson+reviews&kgs=0e755424154859a1&shndl=30&shem=ssim&source=sh/x/loc/osrp/m5/3';
	}
</script>

<head>
	<script src="https://kit.fontawesome.com/bcb26383e6.js" crossorigin="anonymous"></script>
</head>

<body>
	<!-- <Spinner /> -->
	{#if currentLanguage === 'en'}
		<Spinner />
	{:else if currentLanguage === 'my'}
		<SpinnerMalay />
	{/if}
	<div class="min-h-screen w-full flex flex-col items-center justify-center">
		<div class="min-h-screen w-full flex flex-col items-center justify-center">
			<!-- <div class="image-wrapper">
				<img src={Logo} class="w-28 h-28 mb-10" alt="Klinik Menggatal Logo" />
			</div> -->
			<div class="language-switcher">
				<select
					bind:value={currentLanguage}
					class="text-lg p-2 border-2 border-gray-400 rounded-lg focus:outline-none focus:border-blue-500"
				>
					<option value="en">English</option>
					<option value="my">Malay</option>
				</select>
			</div>
			<h1 class="text-2xl sm:text-3xl md:text-4xl text-center mt-10 md:mt-40">
				{translations[currentLanguage].heading}
			</h1>
			{#if $formSubmitted}
				<h1 class="text-xl sm:text-2xl md:text-4xl text-center mt-10 md:mt-20">
					{translations[currentLanguage].exitMessage}
				</h1>
			{:else}
				<div class="flex flex-wrap items-center justify-center mt-10 md:mt-20">
					{#if $star1}
						<i
							class="fa-solid fa-star text-4xl sm:text-6xl md:text-8xl m-2 filled-star-1"
							on:click={clickStar1}
						></i>
					{:else}
						<i
							class="fa-regular fa-star text-4xl sm:text-6xl md:text-8xl m-2 star-1"
							on:click={clickStar1}
						></i>
					{/if}
					{#if $star2}
						<i
							class="fa-solid fa-star text-4xl sm:text-6xl md:text-8xl m-2 filled-star-2"
							on:click={clickStar2}
						></i>
					{:else}
						<i
							class="fa-regular fa-star text-4xl sm:text-6xl md:text-8xl m-2 star-2"
							on:click={clickStar2}
						></i>
					{/if}
					{#if $star3}
						<i
							class="fa-solid fa-star text-4xl sm:text-6xl md:text-8xl m-2 filled-star-3"
							on:click={clickStar3}
						></i>
					{:else}
						<i
							class="fa-regular fa-star text-4xl sm:text-6xl md:text-8xl m-2 star-3"
							on:click={clickStar3}
						></i>
					{/if}
					<i
						class="fa-regular fa-star text-4xl sm:text-6xl md:text-8xl m-2 star-4"
						on:click={clickStar4}
					></i>
					<i
						class="fa-regular fa-star text-4xl sm:text-6xl md:text-8xl m-2 star-5"
						on:click={clickStar5}
					></i>
				</div>

				<div class="flex w-full justify-center items-center recommendation-form hidden mt-10">
					<form
						on:submit|preventDefault={addToRecommendations}
						class="w-full sm:w-3/4 md:w-1/2 bg-white shadow-md rounded-lg p-4 sm:p-6 md:p-8"
					>
						<div class="mb-4 sm:mb-6">
							<label
								for="recommendation"
								class="block text-gray-700 text-sm sm:text-base font-bold mb-2 text-center"
							>
								{translations[currentLanguage].formTitle}
							</label>
							<input
								type="text"
								name="recommendation"
								placeholder={translations[currentLanguage].formPlaceholder}
								class="block w-full rounded-md py-2 px-3 border border-gray-300 h-32"
								required
							/>
						</div>
						<div class="flex justify-center">
							<button
								class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-md"
								type="submit"
							>
								{translations[currentLanguage].formButton}
							</button>
						</div>
					</form>
				</div>

				<h1 class="text-xl sm:text-2xl md:text-4xl text-center mt-10 md:mt-20">
					{translations[currentLanguage].thankYou}
				</h1>
			{/if}
		</div>
	</div></body
>
