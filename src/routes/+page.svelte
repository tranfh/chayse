<script lang="ts">
	import Banner from '$lib/components/banner/banner.svelte';
	import Modal from '$lib/components/modal/modal.svelte';
	import QuestionnaireTemplate from '$lib/components/templates/questionnaire-template.svelte';

	export let type: 'modal' | 'banner' = 'modal';
	export let modalType = 0;
	let showModal = false;

	function toggleModal() {
		showModal = !showModal;
	}

	let template = {
		modal: [
			{
				title: 'Java Newsletter',
				subtitle: 'blah blah blah',
				buttonText: 'Begin Quiz',
				imageText: '10 Coffee Tricks',
				imgSrc:
					'https://static.vecteezy.com/system/resources/previews/030/457/703/large_2x/an-aesthetic-studio-coffee-shop-interior-featuring-a-coffee-cup-and-plant-a-coffee-cup-and-plant-on-a-table-free-photo.jpg',
				onSubmit: handleFormSubmit
			}
		]
	};

	let questions = [
		{
			question: 'What is your favorite color?',
			options: ['Red', 'Green', 'Blue', 'Yellow']
		},
		{
			question: 'What is your favorite animal?',
			options: ['Cat', 'Dog', 'Bird', 'Fish']
		},
		{
			question: 'What is your favorite food?',
			options: ['Pizza', 'Burger', 'Sushi', 'Pasta']
		}
	];

	export function handleFormSubmit(data: { email: string; name: string }) {
		return console.log(data.name, data.email);
	}

	export let modalData = template.modal[modalType];
</script>

<button on:click={toggleModal}>Open Overlay</button>

<div class="container">
	{#if type == 'modal'}
		<Modal {toggleModal} {showModal}>
			<QuestionnaireTemplate
				title={modalData.title}
				subtitle={modalData.subtitle}
				buttonText={modalData.buttonText}
				imageText={modalData.imageText}
				imgSrc={modalData.imgSrc}
				onSubmit={modalData.onSubmit}
				on:questionnaire-complete={() => toggleModal()}
				selectionDisplay={"row"}
				questions={questions}

			/>
		</Modal>
	{/if}
	{#if type == 'banner'}
		<Banner />
	{/if}
</div>

<style>
	button {
		padding: 25px 50px;
		background-color: #6200ea;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}

	.container {
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;
		gap: 10px;
		height: 100vh;
	}
</style>
