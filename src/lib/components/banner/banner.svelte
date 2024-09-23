<script>
	let showBanner = false;

	function toggleBanner() {
		showBanner = !showBanner;
	}

	function handleEscKeyPress(event) {
		if (event.key === 'Escape') {
			showBanner = false;
		}
	}

	function closeOverlayOnOutsideClick(event) {
		if (event.target.classList.contains('overlay')) {
			showBanner = false;
		}
	}
</script>

<button on:click={toggleBanner}>Open Banner</button>

<div
	class="overlay"
	role="dialog"
	aria-labelledby="modal-title"
	aria-modal="true"
	tabindex="-1"
	on:keydown={handleEscKeyPress}
	on:click={closeOverlayOnOutsideClick}
	class:show={showBanner}
>
	<div class="banner-container" class:show={showBanner}></div>
</div>

<style>
	.banner-container {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 200px;
		background-color: rgb(255, 247, 237);
		padding: 20px;
		max-height: 800px;
		max-width: 100rem;
		z-index: 1000;
		box-sizing: border-box;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		transition:
			transform 0.5s ease,
			opacity 0.5s ease; /* Adds smooth transition */
		transform: translateY(100%); /* Start off-screen */
		opacity: 0; /* Hide when off-screen */
	}

	.banner-container.show {
		transform: translateY(0); /* Slide up into view */
		opacity: 1; /* Become visible */
	}

	.overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		background-color: rgba(0, 0, 0, 0.5); /* semi-transparent overlay */
		opacity: 0;
		visibility: hidden;
		transition:
			opacity 0.5s ease,
			visibility 0.5s ease;
		display: flex;
		justify-content: center;
		align-items: flex-end; /* Position the banner at the bottom */
		z-index: 999;
	}

	.overlay.show {
		opacity: 1;
		visibility: visible;
	}

	button {
		padding: 25px 50px;
		background-color: #6200ea;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}
</style>
