<script>
	export let label = '';
	export let inputValue = '';
</script>

<div class="vstack floating-label">
	<input type="text" class="inputValue" bind:value={inputValue} placeholder=" " />
	<label for="inputValue">{label}</label>
</div>

<style>
	/* Floating label styles */
	.floating-label {
		position: relative;
		margin-top: 1rem;
	}

	.floating-label input {
		width: 100%;
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 5px;
		font-size: 1rem;
		box-sizing: border-box;
		background-color: white;
	}

	.floating-label label {
		position: absolute;
		left: 5px;
		top: 50%;
		transform: translateY(-50%);
		background-color: white;
		color: #aaa;
		font-size: 1rem;
		transition: 0.2s ease all;
		pointer-events: none;
		padding: 0 5px;
	}

	.floating-label input:focus ~ label,
	.floating-label input:not(:placeholder-shown) ~ label {
		top: 0.5rem;
		transform: translateY(-100%);
		font-size: 0.85rem;
		color: #b3b3b3;
	}

	input {
		font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', sans-serif;
		font-size: 18px;
		color: #333; /* Optional: Change text color */
	}
</style>
