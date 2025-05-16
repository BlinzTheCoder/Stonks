<script lang="ts">
	import { balance } from '$lib/stores/balance';

	function clearBalance() {
		balance.set(1000);
	}
</script>

<div class="balance-card flex flex-col items-center">
	<div class="flex justify-center bg-[#00ff88] w-40 mb-4 text-[#001100] rounded-md p-1">
		<button onclick={clearBalance}  class="clear-btn w-40">Clear Balance</button>
	</div>
	<p class="label">Current Balance</p>
	<p class="amount">$<span>{$balance}</span></p>
</div>

<style>
	.balance-card {
		position: fixed;
		bottom: 1.5rem;
		right: 1.5rem;
		background-image: radial-gradient(#0f1f0f 1px, transparent 0);
		background-size: 40px 40px;
		background-color: #001100;

		color: #fff;
		padding: 1.5rem 2rem;
		border-radius: 1rem;
		box-shadow: 0 4px 20px rgb(0, 0, 0);
		text-align: center;
		width: 300px;

		font-family: 'Poppins', sans-serif;
		z-index: 1000;
	}

	.label {
		font-size: 1rem;
		color: #bbb;
		font-family: 'Poppins', sans-serif;
		font-weight: 600;
		margin-bottom: 0.5rem;
		letter-spacing: 1px;
		text-transform: uppercase;
	}

	.amount {
		font-size: 2.5rem;
		font-weight: bold;
		color: #00ff88;
	}

	.clear-btn {
		background-color: #001100;
		color: #00ff88;
		border: 2px solid #00ff88;
		border-radius: 0.5rem;
		padding: 0.4rem 1rem;
		font-weight: 700;
		font-family: 'Poppins', sans-serif;
		cursor: pointer;
		transition: background-color 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
	}

	.clear-btn:hover {
		background-color: #00ff88;
		color: #001100;
		box-shadow: 0 0 10px #00ff88;
	}

	.clear-btn:focus {
		outline: none;
		box-shadow: 0 0 10px #00ff88;
	}
</style>
