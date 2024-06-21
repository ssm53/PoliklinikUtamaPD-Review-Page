<script>
	import { loading } from '../stores/store';
</script>

{#if $loading}
	<div class="loader">
		<div class="spinner"></div>
		<div class="loading-text">
			<p>Ini mungkin mengambil masa sehingga 1 minit. Biarkan sahaja ia memuat.</p>
			<p>Anda boleh berjalan ke kereta anda. Ia akan siap pada masa itu!</p>
			<p>TERIMA KASIH!</p>
		</div>
	</div>
{/if}

<style>
	.loader {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: black;
		transition:
			opacity 0.75s,
			visibility 0.75s;
		color: white; /* Ensures text is white */
	}

	.spinner {
		width: 75px;
		height: 75px;
		border: 15px solid lightgrey;
		border-top-color: darkviolet;
		border-radius: 50%;
		animation: loading 0.75s ease infinite;
	}

	.loading-text {
		text-align: center;
		margin-top: 20px; /* Space between spinner and text */
	}

	@keyframes loading {
		from {
			transform: rotate(0turn);
		}
		to {
			transform: rotate(1turn);
		}
	}
</style>
