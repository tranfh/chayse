<script lang="ts">
	import FloatingLabel from '../floating-label/floating-label.svelte';

	export let buttonText: string;
	export let title: string;
	export let subtitle: string;
	export let imageText: string;
	export let onSubmit: (data: { email: string; name: string }) => void;
	export let imgSrc: string;

	let name = '';
	let email = '';

	const handleSubmit = () => {
		if (onSubmit) {
			if (name && email) {
				onSubmit({ name, email });
			}
		}
	};
	/**
	 * @param {{ key: string; preventDefault: () => void; }} event
	 */
	const handleKeyPress = (event) => {
		if (event.key === 'Enter') {
			event.preventDefault(); // Prevent default form submission
			handleSubmit();
		}
	};
</script>

<div class="hstack container">
	<div class="box image">
		<div class="box image-text">
			<h1>{imageText}</h1>
		</div>
		<img src={imgSrc} alt="stock-cafe" />
	</div>
	<form class="hstack form" on:submit|preventDefault={handleSubmit}>
		<div class="vstack">
			<h2>
				{title}
			</h2>
			<p>
				{subtitle}
			</p>
			<FloatingLabel label={'Full Name'} bind:inputValue={name} />
			<FloatingLabel label={'Email Address'} bind:inputValue={email} on:keypress={handleKeyPress} />
			<button class="submit">{buttonText}</button>
		</div>
	</form>
</div>

<style>
	h2,
	p {
		margin: 0;
		text-align: center;
	}

	h2 {
		font-weight: normal;
		font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', sans-serif;
	}

	h1,
	.image-text {
		font-weight: lighter;
		width: 50%;
		text-align: right;
	}

	.form {
		width: 100%;
		padding: 10px;
		display: flex;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	.vstack {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	.hstack {
		flex-direction: row;
	}

	.hstack.container {
		display: flex;
		gap: 5px;
		height: 100%;
		width: 100%;
		border-radius: 0.5rem;
	}

	.box {
		display: flex;
	}

	img,
	.box {
		justify-content: end;
		overflow: hidden;
		flex: 1;
	}

	img {
		object-fit: cover;
		box-sizing: border-box;
		width: 100%;
		height: 100%;
	}

	.box,
	.image {
		border-radius: inherit;
	}

	button {
		margin-top: 1rem;
		height: 2.5rem;
		border: none;
		border-radius: 0.3rem;
		background-color: rgb(77, 133, 166);
		color: white;
	}

	button:hover {
		background-color: rgb(145, 199, 230);
		cursor: pointer;
	}

	.image-text {
		position: absolute;
		color: white;
		z-index: 1;
		font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
		font-weight: lighter;
		font-size: medium;
		padding: 1rem;
		width: fit-content;
	}
</style>
