<script lang="ts">
	import { evaluate } from 'mathjs';
	import { onMount } from 'svelte';

	let value: string = '';
	let result: string = '';

	function select(this: HTMLInputElement, event: Event) {
		this.select();
	}

	async function calculate() {
		result = await evaluate(value);

		chrome.storage.local.set({ equation: value, result }).then(() => {
			console.log('Value is set to ' + result);
		});
	}

	onMount(() => {
		chrome.storage.local.get(['equation', 'result']).then((store) => {
			const eq = store['equation'];
			const res = store['result'];

			value = eq || '';
			result = res || 'Result';
		});
	});
</script>

<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css" />
	<link rel="stylesheet" href="popup.css" />
</svelte:head>

<div class="container">
	<h1>Calculator</h1>
	<form on:submit|preventDefault={calculate}>
		<input type="text" placeholder="1 + 2" bind:value on:click={select} />
	</form>

	<p>{result}</p>
</div>
