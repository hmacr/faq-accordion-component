<script lang="ts">
	<!-- import ArrowDownIcon from "../assets/icon-arrow-down.svg"; -->
  	import DesktopImage from "./DesktopImage.svelte";
  	import MobileImage from "./MobileImage.svelte";
	import faq_json from "../assets/faq.json";

	import { useMediaQuery } from "../lib/media_query";

	let is_md = useMediaQuery('(min-width: 768px)');

	let prev: HTMLElement;

	function handleClick(e: Event) {
		if (prev) {
			const question = prev.querySelector('.question') as HTMLElement;
			const arrow = prev.querySelector('.arrow') as HTMLElement;
			const ans = prev.querySelector('.answer') as HTMLElement;
			question.classList.add('text-very-dark-grayish-blue');
			question.classList.remove('text-very-dark-desaturated-blue', 'font-bold');
			arrow.classList.remove('rotate-180');
			ans.classList.add('hidden');
		}
		const curr = (e.currentTarget as HTMLElement).parentElement as HTMLElement;
		const question = curr.querySelector('.question') as HTMLElement;
		const arrow = curr.querySelector('.arrow') as HTMLElement;
		const ans = curr.querySelector('.answer') as HTMLElement;
		question.classList.remove('text-very-dark-grayish-blue');
		question.classList.add('text-very-dark-desaturated-blue', 'font-bold');
		arrow.classList.add('rotate-180');
		ans.classList.remove('hidden');
		prev = curr;
	}
</script>

<div class="w-[400px] md:w-[900px] md:flex font-kumbh-sans text-sm p-6 bg-white rounded-3xl shadow-xl">
	<!-- Image -->
	{#if $is_md}
	<DesktopImage />
	{:else}
	<MobileImage />
	{/if}
	<!-- Content -->
	<div class="mt-16 md:w-[50%] md:p-8">
		<h1 class="font-bold text-3xl tracking-wide text-center md:text-left ml-4 text-very-dark-desaturated-blue">FAQ</h1>
		<ul class="mt-1 py-4">
			{#each faq_json as faq}
			<li class="m-4 pb-4 border-b border-b-light-grayish-blue">
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div class="flex justify-between items-center text-very-dark-grayish-blue hover:text-soft-red hover:cursor-pointer
					transition-colors" on:click={handleClick}>
					<h4 class="question">{faq.q}</h4>
					<img src={ArrowDownIcon} alt="arrow" class="arrow w-3 h-2">
				</div>
				<p class="answer mt-3 pr-6 text-dark-grayish-blue hidden">{faq.a}</p>
			</li>
			{/each}
		</ul>
	</div>
</div>
