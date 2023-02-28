<script>
	import './styles.css';
	import {isChosenSystem} from "../lib/store"

	/**
	 * @type {boolean}
	 */
	let isChosenBinary;

	isChosenSystem.subscribe(value => {
		isChosenBinary = value;
	});

</script>

<div class="app">
	<header class="py-3">
		<nav class="flex justify-center ">
			<div class="border rounded relative min-w-[320px]">
				<div class="absolute bg-blue-500 w-[160px] h-[44px] top-0 transition-all {isChosenBinary ? '': 'translate-x-full'}"></div>
				<button 
					class="uppercase text-sm py-3 min-w-[160px] relative text-center transition-all {isChosenBinary && 'text-white'}"
					on:click={() => isChosenSystem.update(n => n = true)}
				>Binary Operation</button>
				<button 
					class="uppercase text-sm py-3 min-w-[160px] relative text-center transition-all {!isChosenBinary && 'text-white'}"
					on:click={() => isChosenSystem.update(n => n = false)}
				>Number System</button>
			</div>
		</nav>
	</header>
	<main>
		<slot />
	</main>
</div>

	