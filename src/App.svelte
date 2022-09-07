<script>
	import Upload from './lib/Upload.svelte'
</script>

<main>
	<div class="wrapper flex">
		<h1 class="title flex">Mini-Corner CSV Cleaner</h1>

		<section class="hero flex">
			<div class="upload flex">
				<Upload></Upload>
			</div>
		</section>
	</div>
</main>

<style>
	.flex {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.wrapper {
		height: 100vh;
		width: 100vw;
		margin: 0 auto;
		flex-direction: column;
	}

	.title {
		display: none;
	}
	
	.upload {
		width: 90vw;
		height: 90vh;
		border-radius: 30px;
		position: relative;
		flex-direction: column;
		font-size: 2rem;
		background-color: #646cff;
	}

	@media (min-width: 768px) {
		.title {
			display: flex;
			width: 90vw;
			height: 10vh;
			font-size: clamp(1rem, 10vw, 2.5rem);
			margin: 0 0 50px 0;
			border-radius: 30px;
			background-color: #646cff;
		}

		.upload {
			height: 70vh;
		}
	}
</style>