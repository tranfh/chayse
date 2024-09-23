<script>
	export let showModal = false;
	export let toggleModal;

	function handleEscKeyPress(event) {
		if (event.key === 'Escape') {
			showModal = false;
		}
	}

	function closeOverlayOnOutsideClick(event) {
		if (event.target.classList.contains('overlay')) {
			showModal = false;
		}
	}
</script>

<div
	class="overlay"
	role="dialog"
	aria-labelledby="modal-title"
	aria-modal="true"
	tabindex="-1"
	on:keydown={handleEscKeyPress}
	on:click={closeOverlayOnOutsideClick}
	class:show={showModal}
>
	<div class="modal" class:show={showModal}>
			<div class="top-hstack">
				<button class="close-btn" on:click={toggleModal} aria-label="Close Overlay">X</button>
			</div>
			<slot></slot>
	</div>
</div>

<style>
	.overlay {
		position: fixed; /* Stay in place */
		top: 0; /* Full height */
		width: 100%; /* Full width */
		height: 100%; /* Full screen */
		background-color: rgba(0, 0, 0, 0.7); /* Black background with transparency */
		z-index: 999; /* Make sure it sits on top */
		display: flex; /* Center the content */
		align-items: center;
		justify-content: center;
		visibility: hidden;
		transition:
			opacity 0.5s ease,
			visibility 0.5s ease;
		opacity: 0;
	}

	.overlay.show {
		opacity: 1;
		visibility: visible;
	}
	.modal {
		background-color: white;
		border-radius: 10px;
		width: 50rem;
		height: 35rem;
		max-width: 50rem; /* Max width of the content */
		max-height: 40rem;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		opacity: 0;
		z-index: 1000;
		transition: opacity 0.5s ease; /* Adds smooth transition */
	}

	.modal.show {
		opacity: 1;
		visibility: visible;
	}

	.close-btn {
		position: absolute;
		background-color: unset;
		color: rgb(0, 0, 0);
		padding: 10px;
		border: none;
		cursor: pointer;
		border-radius: 50%;
		font-size: 1rem;
	}

	.close-btn:hover {
		color: rgb(234, 223, 223);
	}

	.top-hstack {
		display: flex;
		flex-direction: row;
		justify-content: end;
	}
</style>
