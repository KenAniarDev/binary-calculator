<script>
	// @ts-nocheck

	import {
		Listbox,
		ListboxButton,
		ListboxOptions,
		ListboxOption
	} from '@rgossiaux/svelte-headlessui';

	const people = [
		{ id: 1, name: 'Division' },
		{ id: 2, name: 'Multiplication' },
		{ id: 3, name: 'Subtraction' },
		{ id: 4, name: 'Addition' },
		{ id: 5, name: 'Negative' }
	];

	let selectedOperation = people[0];

	let calculatedBinary = '';

	const handleSubmit = (e) => {
		const { firstOperand: first, secondOperand: second } = e.target.elements;

		let firstOperand = parseInt(first.value, 2);
		let secondOperand = parseInt(second.value, 2);

		switch (selectedOperation.id) {
			case 1:
				calculatedBinary = (firstOperand / secondOperand).toString(2);
				break;
			case 2:
				calculatedBinary = (firstOperand * secondOperand).toString(2);
				break;
			case 3:
				calculatedBinary = (firstOperand - secondOperand).toString(2);
				break;
			case 4:
				calculatedBinary = (firstOperand + secondOperand).toString(2);
				break;
			case 5:
				const invertedBinaryString = first.value
					.split('')
					.map((bit) => (bit === '0' ? '1' : '0'))
					.join(''); // Invert all the bits
				calculatedBinary = (parseInt(invertedBinaryString, 2) + 1).toString(2);
				break;
			default:
				calculatedBinary = (firstOperand + secondOperand).toString(2);
		}
	};
</script>

<form class="max-w-[320px] mx-auto mt-5" on:submit|preventDefault={handleSubmit}>
	<input
		type="text"
		name="firstOperand"
		id="firstOperand"
		pattern="[01]+"
		title="Please enter only 1's and 0's"
		class="border w-full py-1 px-2"
		required
	/>

	<input
		type="text"
		name="secondOperand"
		id="secondOperand"
		pattern="[01]+"
		title="Please enter only 1's and 0's"
		class="border w-full py-1 px-2 {selectedOperation.id == 5 && 'hidden'}"
		required={selectedOperation.id != 5}
	/>

	<div class="flex">
		<Listbox
			value={selectedOperation}
			on:change={(e) => (selectedOperation = e.detail)}
			class="border w-1/2 py-1 px-2 text-center relative"
		>
			<ListboxButton>{selectedOperation.name}</ListboxButton>
			<ListboxOptions class="absolute bg-white w-full shadow space-y-1 py-2">
				{#each people as person (person.id)}
					<ListboxOption value={person} class="cursor-pointer">
						{person.name}
					</ListboxOption>
				{/each}
			</ListboxOptions>
		</Listbox>
		<button type="submit" class="border w-1/2 py-1 px-2">Calculate</button>
	</div>
	<div class="{calculatedBinary.length > 0 ? 'block' : 'hidden'}border w-full py-1 px-2">
		{calculatedBinary}
	</div>
</form>
