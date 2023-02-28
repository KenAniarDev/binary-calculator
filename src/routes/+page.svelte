<script>
	import BinaryOperations from "./BinaryOperations.svelte";
	import NumberSystem from "./NumberSystem.svelte";
	import {isChosenSystem} from "../lib/store"

	/**
	 * @type {boolean}
	 */
	 let isChosenBinary;

	isChosenSystem.subscribe(value => {
		isChosenBinary = value;
	});
</script>

<svelte:head>
	<title>Binary Calculator</title>
	<meta name="description" content="Binary Calculator" />
</svelte:head>

{#if isChosenBinary}
	<BinaryOperations />
{:else}
	<NumberSystem />
{/if}