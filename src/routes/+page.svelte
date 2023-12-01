<script lang="ts">
	import { evaluate } from 'mathjs';

	let value: string = '';
	let result: string = '';

	function select(this: HTMLInputElement, event: Event) {
		this.select();
	}

	function calculate() {
		result = evaluate(value);
	}
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
