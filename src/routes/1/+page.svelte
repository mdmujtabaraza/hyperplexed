<script lang="ts">
	let cards = [
		{ title: 'Card 1' },
		{ title: 'Card 2' },
		{ title: 'Card 3' },
		{ title: 'Card 4' },
		{ title: 'Card 5' },
		{ title: 'Card 6' }
	];
	const handleOnPointerMove = (e) => {
		for (const card of document.getElementsByClassName('card')) {
			const rect = card.getBoundingClientRect(),
				x = e.clientX - rect.left,
				y = e.clientY - rect.top;

			card.style.setProperty('--mouse-x', `${x}px`);
			card.style.setProperty('--mouse-y', `${y}px`);
		}
	};
	// const handleOnMouseMove = (e) => {
	// 	const { currentTarget: target } = e;

	// 	const rect = target.getBoundingClientRect(),
	// 		x = e.clientX - rect.left,
	// 		y = e.clientY - rect.top;

	// 	target.style.setProperty('--mouse-x', `${x}px`);
	// 	target.style.setProperty('--mouse-y', `${y}px`);
	// };

	// const cards = document.querySelectorAll('.card');
	// for (const card of cards) {
	// 	card.onpointermove = (e) => handleOnMouseMove(e);
	// }
</script>

<main>
	<div id="cards" on:pointermove={handleOnPointerMove}>
		{#each cards as card, i}
			<div class="card">
				<div class="card-content">{card.title}</div>
			</div>
		{/each}
	</div>
</main>

<style lang="scss">
	:root {
		--bg-color: rgb(20, 20, 20);
		--card-color: rgb(23, 23, 23);
	}
	main {
		height: 100vh;
		background-color: var(--bg-color);
		display: flex;
		justify-content: center;
		align-items: center;
		// margin: 0px;
		// overflow: hidden;
		// padding: 0px;
	}
	#cards {
		display: flex;
		flex-wrap: wrap;
		gap: 8px;
		// max-width: 100%;
		width: 60%;
		&:hover {
			.card::after {
				opacity: 1;
			}
		}
	}
	.card {
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: rgba(255, 255, 255, 0.02);
		// border: 1px solid rgba(255, 255, 255, 0.1);
		height: 260px;
		width: 300px;
		cursor: pointer;
		position: relative;
		// border-radius: 10px;
		&:hover {
			&:before {
				opacity: 1;
			}
		}
		&:before,
		&:after {
			border-radius: inherit;
			content: '';
			height: 100%;
			left: 0px;
			top: 0px;
			opacity: 0;
			transition: opacity 500ms;
			position: absolute;
			width: 100%;
		}
		&:before {
			background: radial-gradient(
				800px circle at var(--mouse-x) var(--mouse-y),
				rgba(255, 255, 255, 0.06),
				transparent 40%
			);
			z-index: 3;
		}
		&:after {
			background: radial-gradient(
				600px circle at var(--mouse-x) var(--mouse-y),
				rgba(255, 255, 255, 0.4),
				transparent 40%
			);
			z-index: 1;
		}
		.card-content {
			// height: calc(100% - 2px);
			// width: calc(100% - 2px);
			// margin: 1px;
			background-color: var(--card-color);
			border-radius: inherit;
			display: flex;
			flex-direction: column;
			flex-grow: 1;
			position: absolute;
			inset: 1px;
			padding: 10px;
			z-index: 2;
		}
	}
</style>
