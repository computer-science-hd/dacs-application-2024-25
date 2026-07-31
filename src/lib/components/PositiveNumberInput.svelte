<script lang="ts">
	import Input from 'flowbite-svelte/Input.svelte';
	
	export let value: number | null;

	let inputValue = value?.toString() ?? '';
	
	//function handleInput() {
	function handleInput(event: Event) {
		inputValue = (event.currentTarget as HTMLInputElement).value;

		// Allow an empty value while editing
		if (inputValue === '') {
			value = null;
			return;
		}
		
		/* check if initialized */
		/*if (!value) return*/
		/*if (value === null || value === undefined || value === '') return;*/
		
		/* check if number */
		/*if (Number.isNaN(Number(value))) {
			value = 0;
			return 
		}*/
		
		/* check if gt 0 */
		/*if (value < 0 ) { 
			value = 0;
			return 
		}*/

		const parsedValue = Number(inputValue.replace(',', '.'));

		if (!Number.isNaN(parsedValue) && parsedValue >= 0) {
			value = parsedValue;
		}

		/* strips leading zeros */
		/*value = Number(value);*/
	}

	function handleBlur() {
		if (value === null) {
			inputValue = '';
			return;
		}

		inputValue = value.toString();
	}
	
</script>

<!--<Input type="text" bind:value={value} on:input={handleInput} {...$$restProps} />-->
<Input type="text" inputmode="decimal" value={inputValue} on:input={handleInput} on:blur={handleBlur} {...$$restProps}/>
