<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let question: string = 'What is your favorite color?';
	export let options: string[] = ['Option 1', 'Option 2', 'Option 3', 'Option 4'];

	const dispatch = createEventDispatcher();

	function handleOptionClick(option: string) {
		dispatch('answer', option); // Emit the selected option
	}

	// Limit options to a maximum of 4
	$: limitedOptions = options.slice(0, 4);
</script>

<div class="question-container">
	<div class="question-text">{question}
        <div class="divider"></div>
    </div>
	<div
		class="selections"
		style={`grid-template-columns: repeat(${Math.min(limitedOptions.length, 2)}, 1fr);`}
	>
		{#each limitedOptions as option, index}
			<div class="option {`option-${index + 1}`}" on:click={() => handleOptionClick(option)}>
				{option}
			</div>
		{/each}
	</div>
</div>

<style>
	.question-container {
		display: flex;
		flex-direction: column;
        justify-content: space-between;
		width: 100%;
        height:100%;
		padding: 2rem;
		border-radius: 10px;
		background-color: #fff; /* Background color of the modal */
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        box-sizing: border-box;
	}

	.question-text {
		font-size: 20px;
		font-weight: lighter;
		margin-bottom: 20px;
		text-align: center;
        color:  #1b82bd;
	}

	.selections {
		display: grid;
		gap: 10px;
		width: 100%;
        height: 100%;
        margin-bottom: 1rem;
	}

	.option {
		padding: 15px;
		border-radius: 8px; /* Rounded edges */
		text-align: center;
		cursor: pointer;
		transition: background-color 0.3s ease;
        color:  #1b82bd;
        display: flex;
        justify-content: center;
        align-items: center;
	}

	.option:hover {
		background-color: #5eb0df; /* Change color on hover */
	}

	/* Option colors (optional) */
	.option-1 {
		background-color: #f1f1f1;
	}
	.option-2 {
		background-color: #f1f1f1;
	}
	.option-3 {
		background-color: #f1f1f1;
	}
	.option-4 {
		background-color: #f1f1f1;
	}

    .divider {
        width: 100%;
        border-bottom: 1px solid #88d0fa;
        margin: 2rem 0rem;
    }

   
</style>
