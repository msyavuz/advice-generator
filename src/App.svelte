<script>
	import axios from "axios";
	import { onMount } from "svelte";
	let advice = {};

	const getAdvice = async () => {
		try {
			let res = await axios.get(
				"https://api.adviceslip.com/advice?t=" + Math.random()
			);
			return res.data.slip;
		} catch (error) {
			console.error(error);
		}
	};
	const newAdvice = async () => {
		advice = await getAdvice();
	};
	onMount(newAdvice);
</script>

<main class="flex flex-col justify-center place-items-center w-screen h-screen">
	<div
		class="advice-container container grid grid-rows-6 justify-center place-items-center rounded-3xl lg:w-1/3 sm:w-full h-96 font-bold text-2xl p-8"
	>
		<p
			class="advice-no container flex justify-center place-items-center row-span-1"
		>
			Advice #{advice.id}
		</p>
		<div class="container advice row-span-3">
			"{advice.advice}"
		</div>
		<div
			class="line-break w-full h-px flex justify-center place-items-center gap-4"
		/>
		<div
			class="flex justify-center place-items-center button-container container fixed mt-96 w-12 aspect-square rounded-full"
		>
			<button class="" on:click={newAdvice}>
				<svg width="24" height="24" xmlns="http://www.w3.org/2000/svg"
					><path
						d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z"
						fill="#202733"
					/></svg
				>
			</button>
		</div>
	</div>
</main>

<style lang="postcss" global>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;

	main {
		background-color: hsl(218, 23%, 16%);
		color: hsl(193, 38%, 86%);
	}
	.advice-no {
		color: hsl(150, 100%, 66%);
	}
	.advice-container {
		background-color: hsl(217, 19%, 38%);
		border: hsl(217, 19%, 38%);
	}
	.button-container {
		background-color: hsl(150, 100%, 66%);
	}
	.button-container:hover,
	.button-container:active {
		box-shadow: 0 0 40px 0.2em hsl(150, 100%, 66%);
	}
	.line-break {
		background-color: hsl(193, 38%, 86%);
	}
	.first-box {
		background-color: hsl(217, 19%, 38%);
	}
</style>
