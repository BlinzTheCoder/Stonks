<script lang="ts">
	import Invest from '$lib/components/Invest.svelte';
	import Settings from '$lib/components/Settings.svelte';
	import Info from '$lib/components/Info.svelte';
	import Instructions from '$lib/components/Instructions.svelte';
	import Wallet from '$lib/components/Wallet.svelte';
	import { onMount } from 'svelte';

	type State = 'invest' | 'settings' | 'info' | 'instructions';
	let gameState: State = 'invest';

	onMount(() => {
		console.log('Component mounted');
	});
</script>

<main>
	<script lang="ts">
	</script>

	<div class="fixed top-0 right-0 left-0 flex w-full justify-between bg-white px-4 py-2 shadow">
		<div class="flex items-center">
			<img src="Logo.png" alt="Logo" class="mr-2 h-8 w-12" />
			<p class="heading">Stonks!</p>
		</div>
		<div>
			<button
				aria-label="Instructions"
				class="action-buttons instructions-btn"
				onclick={() => (gameState = 'instructions')}><i class="fa-solid fa-book fa-lg"></i></button
			>
			<button aria-label="Info" class="action-buttons info-btn" onclick={() => (gameState = 'info')}
				><i class="fa-solid fa-info fa-lg"></i></button
			>
		</div>
	</div>
	{#if gameState === 'invest'}
		<Invest />
		<Wallet />
	{:else if gameState === 'settings'}
		<Settings />
	{:else if gameState === 'info'}
		<Info />
	{:else if gameState === 'instructions'}
		<Instructions />
	{/if}
</main>

<style>
	.heading {
		font-size: 1.8rem;
		font-family: 'Poppins', sans-serif;
		font-weight: 600;
		color: black;
	}

	.action-buttons {
		width: 3.5rem;
		color: white;
		border: none;
		padding: 0.5rem 1rem;
		border-radius: 0.5rem;
		margin-left: 0.5rem;
		font-weight: bold;
		font-family: 'Noto Sans TC', sans-serif;
		font-size: 1rem;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	/* Instructions (light blue glow) */
	.instructions-btn {
		background-color: #007acc;
		box-shadow: 0 0 10px 2px rgba(0, 174, 255, 0.5);
	}
	.instructions-btn:hover {
		background-color: #0099ff;
		box-shadow: 0 0 15px 5px rgba(0, 174, 255, 0.8);
	}

	/* Info (orange glow) */
	.info-btn {
		background-color: #db6e00;
		box-shadow: 0 0 10px 2px rgba(255, 140, 0, 0.5);
	}
	.info-btn:hover {
		background-color: #ff8000;
		box-shadow: 0 0 15px 5px rgba(255, 140, 0, 0.8);
	}

	/* Settings (yellow glow) */
	.settings-btn {
		background-color: #d4aa00;
		box-shadow: 0 0 10px 2px rgba(255, 230, 0, 0.5);
	}
	.settings-btn:hover {
		background-color: #ffcc00;
		box-shadow: 0 0 15px 5px rgba(255, 230, 0, 0.8);
	}
</style>
