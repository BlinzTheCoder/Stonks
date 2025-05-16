<script lang="ts">
	import Invest from '$lib/components/Invest.svelte';
	import Wallet from '$lib/components/Wallet.svelte';
	import { onMount } from 'svelte';

	type State = 'invest' | 'info' | 'instructions';
	let gameState: State = 'invest';

	onMount(() => {
		console.log('Component mounted');
	});
</script>

<main>
	<!-- Info content -->
	{#if gameState === 'info'}
		<div class="instructions-container">
			<h2>ℹ️ Info</h2>
			<ul>
				<li>This website is made for coolestprojects.org - 2025</li>
				<li>Stonks! is inspired by SDG - 8 (Economic WellBeing)</li>
				<li>This website is made using Sveltekit, and Tailwind CSS</li>
				<li>I tried my best to make the design the best that I could</li>
				<li>I wish everyone good luck with their submissions!</li>
			</ul>
		</div>
	{/if}

	{#if gameState === 'instructions'}
		<div class="instructions-container">
			<h2>🎮 How to Play</h2>
			<ul>
				<li>A random stock is shown with its name and price.</li>
				<li>Click <strong>↑</strong> if you think the stock will go up.</li>
				<li>Click <strong>↓</strong> if you think the stock will go down.</li>
				<li>If you guess right, you gain the stock's price in virtual money.</li>
				<li>If you're wrong, you lose that much.</li>
			</ul>

			<h3>💡 Tips</h3>
			<ul>
				<li>The game is based on luck, so there’s no pattern to follow.</li>
				<li>Track your profit and loss with the sparkline in the middle.</li>
				<li>Your balance is saved automatically in your browser.</li>
				<li>Play smart — don’t go all in on red streaks!</li>
			</ul>
		</div>
	{/if}

	<div class="fixed top-0 right-0 left-0 flex w-full justify-between bg-white px-4 py-2 shadow">
		<div class="flex items-center">
			<img src="Logo.png" alt="Logo" class="mr-2 h-8 w-12" />
			<p class="heading">Stonks!</p>
		</div>
		<div>
			<button
				aria-label="Instructions"
				class="action-buttons instructions-btn"
				onclick={() => (gameState = 'instructions')}
			>
				<i class="fa-solid fa-book fa-lg"></i>
			</button>
			<button
				aria-label="Info"
				class="action-buttons info-btn"
				onclick={() => (gameState = 'info')}
			>
				<i class="fa-solid fa-info fa-lg"></i>
			</button>
		</div>
	</div>

	{#if gameState === 'invest'}
		<Invest />
		<Wallet />
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

	.instructions-container {
		max-width: 480px;
		margin: 10% auto;
		padding: 1.5rem 2rem;
		background: #f9f9f9;
		border-radius: 8px;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
		color: #222;
		font-family: 'Poppins', sans-serif;
		line-height: 1.6;
	}

	.instructions-container h2 {
		font-weight: 700;
		font-size: 1.8rem;
		margin-bottom: 1rem;
		color: #333;
		text-align: center;
	}

	.instructions-container h3 {
		font-weight: 600;
		font-size: 1.2rem;
		margin-top: 2rem;
		margin-bottom: 0.6rem;
		color: #555;
	}

	.instructions-container ul {
		padding-left: 1.2rem;
		margin: 0;
		list-style-type: disc;
	}

	.instructions-container li {
		margin-bottom: 0.5rem;
		font-size: 1rem;
	}

	.instructions-container strong {
		color: #000;
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
</style>
