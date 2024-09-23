<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let question: string = 'What is your favorite color?';
	export let options: string[] = ['Option 1', 'Option 2', 'Option 3', 'Option 4'];
	export let selectionDisplay: 'row' | 'grid';
	const dispatch = createEventDispatcher();

	function handleOptionClick(option: string) {
		dispatch('answer', option); // Emit the selected option
	}

	// Limit options to a maximum of 4
	$: limitedOptions = options.slice(0, 4);
</script>

<div class="question-container">
	<div class="question-text">
		{question}
		<div class="divider"></div>
	</div>
	{#if selectionDisplay === 'grid'}
		<div
			class="selections-grid"
			style={`grid-template-columns: repeat(${Math.min(limitedOptions.length, 2)}, 1fr);`}
		>
			{#each limitedOptions as option, index}
				<div
					class="option option-grid {`option-${index + 1}`}"
					on:click={() => handleOptionClick(option)}
				>
					{option}
				</div>
			{/each}
		</div>
	{/if}
	{#if selectionDisplay === 'row'}
		<div class="selections-row">
			{#each limitedOptions as option, index}
				<div class="option option-row" on:click={() => handleOptionClick(option)}>
					<span class="label">{index+1})</span>
					{option}
				</div>
			{/each}
		</div>
	{/if}
</div>

<style>
	.question-container {
		display: flex;
		flex-direction: column;
		width: 100%;
		height: 100%;
		padding: 2rem;
		border-radius: 10px;
		background-color: #fff; /* Background color of the modal */
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		box-sizing: border-box;
	}

	.question-text {
		font-size: 25px;
		font-weight: lighter;
		text-align: center;
		color: #1b82bd;
	}

	.selections-grid {
		display: grid;
		gap: 10px;
		width: 100%;
		height: 100%;
		margin-bottom: 1rem;
		background-color: white;
	}

	.selections-row {
		display: flex;
		flex-direction: column;
		gap: 10px;
		width: 100%;
		margin-bottom: 1rem;
		background-color: white;

	}

	.option {
		padding: 15px;
		font-size: 20px;
		cursor: pointer;
		transition: background-color 0.3s ease;
		color: #1b82bd;
		display: flex;
	}

	.option-grid {
		text-align: center;
		justify-content: center;
		align-items: center;
		border-radius: 8px;
		background-color: #f1f1f1;;
	}

	.option-row {
		text-align: left;
		border: 1px solid #1b82bd;
		padding: 1.5rem;
		margin: 0px 6rem;
	}

	.option:hover {
		background-color: #5eb0df; /* Change color on hover */
		color: white;
	}

	.divider {
		width: 100%;
		border-bottom: 1px solid #88d0fa;
		margin: 2rem 0rem;
	}

	.label {
        margin-right: 10px;
    }
</style>
