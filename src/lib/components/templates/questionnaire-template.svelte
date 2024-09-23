<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import PiiModal from '../modal/pii-modal.svelte';
	import QuestionModal from '../modal/question-modal.svelte';

	export let buttonText: string;
	export let title: string;
	export let subtitle: string;
	export let imageText: string;
	export let onSubmit: (data: { email: string; name: string }) => void;
	export let imgSrc: string;
	export let selectionDisplay: "row" | "grid";
	export let questions: {question: string, options: string[]}[] = [];
	const dispatch = createEventDispatcher();

	let currentPage: 'pii' | 'question' = 'pii';

	function handlePiiSubmit(data: { email: string; name: string }) {
		console.log('PII Submitted:', data);
		onSubmit(data);
		currentPage = 'question'; // Move to the question page
	}

	let currentQuestionIndex = 0;

	function handleAnswer(answer: string) {
		console.log('Selected answer:', answer);
		if (currentQuestionIndex < questions.length - 1) {
			currentQuestionIndex += 1;
		} else {
			dispatch('questionnaire-complete');
			console.log('All questions answered!');
			setTimeout(() => {
				(currentPage = 'pii'), (currentQuestionIndex = 0);
			}, 1000);
		}
	}
</script>

<div>
	{#if currentPage === 'pii'}
		<PiiModal {title} {subtitle} {buttonText} {imageText} {imgSrc} onSubmit={handlePiiSubmit} />
	{:else if currentPage === 'question'}
		<QuestionModal
			question={questions[currentQuestionIndex].question}
			options={questions[currentQuestionIndex].options}
			on:answer={(event) => handleAnswer(event.detail)}
			selectionDisplay={selectionDisplay}
		/>
	{/if}
</div>

<style>
	div {
		height: 100%;
	}
</style>
