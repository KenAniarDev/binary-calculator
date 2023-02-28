<script>
	// @ts-nocheck

	const handleSubmit = () => {};
	let binary = '';
	let decimal = undefined;
	let hexa = undefined;
	let octa = undefined;
	let changedInput = 0;

	const filterBinary = (bin) => {
		return bin
			.split('')
			.filter((e) => {
				return e === '1' || e === '0';
			})
			.join('');
	};

	$: {
		binary = filterBinary(binary);

		if (changedInput === 1) {
			decimal = parseInt(binary, 2);
			hexa = parseInt(binary, 2).toString(16).toUpperCase();
			octa = parseInt(binary, 2).toString(8).toUpperCase();
		} else if (changedInput === 2) {
			binary = decimal.toString(2);
			hexa = decimal.toString(16).toUpperCase();
			octa = decimal.toString(8).toUpperCase();
		} else if (changedInput === 3) {
			binary = parseInt(hexa, 16).toString(2);
			decimal = parseInt(hexa, 16);
			octa = decimal.toString(8).toUpperCase();
		} else if (changedInput === 4) {
			binary = parseInt(octa, 8).toString(2);
			decimal = parseInt(octa, 8);
			hexa = decimal.toString(16).toUpperCase();
		}
	}
</script>

<form class="max-w-[320px] mx-auto mt-5" on:submit|preventDefault={handleSubmit}>
	<div class="flex items-center gap-1">
		<label for="binary" class="min-w-[60px]">Binary</label>
		<input
			type="text"
			title="Please enter only 1's and 0's"
			class="border w-full py-1 px-2 "
			bind:value={binary}
			on:keydown={() => (changedInput = 1)}
		/>
	</div>
	<div class="flex items-center gap-1">
		<label for="decimal" class="min-w-[60px]">Decimal</label>
		<input
			type="number"
			title="Please enter only 1's and 0's"
			class="border w-full py-1 px-2"
			bind:value={decimal}
			on:keydown={() => (changedInput = 2)}
		/>
	</div>
	<div class="flex items-center gap-1">
		<label for="hexa" class="min-w-[60px]">Hexa</label>
		<input
			type="text"
			title="Please enter only 1's and 0's"
			class="border w-full py-1 px-2"
			bind:value={hexa}
			on:keydown={() => (changedInput = 3)}
		/>
	</div>
	<div class="flex items-center gap-1">
		<label for="octa" class="min-w-[60px]">Octa</label>
		<input
			type="number"
			title="Please enter only 1's and 0's"
			class="border w-full py-1 px-2"
			bind:value={octa}
			on:keydown={() => (changedInput = 4)}
		/>
	</div>
</form>
