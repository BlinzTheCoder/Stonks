<script lang="ts">
  import { onMount } from 'svelte';
  import { balance as balanceStore } from '$lib/stores/balance';

  type Stonk = { name: string; fullName: string; price: number };

  const allStonks: Stonk[] = [
    { name: 'CHC', fullName: 'CheeseCoin', price: 150 },
    { name: 'BBK', fullName: 'BananaBucks', price: 200 },
    { name: 'DND', fullName: 'DonutDrive', price: 300 },
    { name: 'ICE', fullName: 'IceCorporation', price: 250 },
    { name: 'LOL', fullName: 'LaughOutLoudCoin', price: 420 },
    { name: 'BRB', fullName: 'BeRightBackToken', price: 69 },
    { name: 'OMG', fullName: 'OhMyGold', price: 777 },
    { name: 'WTF', fullName: 'WhatTheFinance', price: 123 },
    { name: 'YOLO', fullName: 'YouOnlyLiveOnceCoin', price: 888 },
    { name: 'FOMO', fullName: 'FearOfMissingOutToken', price: 999 }
  ];

  let currentStonk: Stonk;
  let resultMessage = '';
  let sparkline: number[] = [];

  onMount(() => {
    const saved = localStorage.getItem('balance');
    balanceStore.set(saved ? +saved : 0);

    balanceStore.subscribe((val) => {
      localStorage.setItem('balance', String(val));
    });

    currentStonk = getRandomStonk();
  });

  function getRandomStonk(): Stonk {
    return allStonks[Math.floor(Math.random() * allStonks.length)];
  }

  function invest(direction: 'up' | 'down') {
    const win = Math.random() > 0.5;
    const change = (win ? 1 : -1) * currentStonk.price;

    sparkline = [...sparkline, win ? 1 : -1].slice(-59);

    resultMessage = win
      ? `Correct! You earned $${currentStonk.price}`
      : `Wrong! You lost $${currentStonk.price}`;

    balanceStore.update((b) => b + change);
    currentStonk = getRandomStonk();
  }
</script>

{#if currentStonk}
  <div class="invest-container">
    <div class="invest-window px-2 py-1 text-white">
      <p class="stonk-info select-none">
        {currentStonk.name} ({currentStonk.fullName})
      </p>
      <p class="stonk-extra select-none">Price: ${currentStonk.price}</p>
      <p class="stonk-extra select-none">{resultMessage}</p>

      <!-- profit/loss sparkline centered -->
      <div class="sparkline">
        {#each sparkline as val, i (i)}
          <div
            class="spark-bar"
            class:up={val === 1}
            class:down={val === -1}
            title={val === 1 ? 'Profit' : 'Loss'}
          ></div>
        {/each}
      </div>
    </div>

    <div class="actions">
      <button class="invest-actions" on:click={() => invest('up')}>↑</button>
      <button class="invest-actions" on:click={() => invest('down')}>↓</button>
    </div>
  </div>
{/if}

<style>
  .invest-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
    background: linear-gradient(white, rgb(218, 218, 218));
  }

  .invest-window {
    width: 50%;
    height: 56%;
    background-color: #001100;
    box-shadow: 0 4px 20px rgb(0, 0, 0);
    border-radius: 0.3rem;
    position: relative;
    background-image:
      linear-gradient(to right, rgba(255, 255, 255, 0.06) 1px, transparent 1px),
      linear-gradient(to bottom, rgba(255, 255, 255, 0.06) 1px, transparent 1px);
    background-size: 24px 24px;
    padding: 1rem;
    overflow-x: auto;
  }

  .stonk-info {
    font-size: 1.5rem;
    font-family: 'Poppins', sans-serif;
    font-weight: 600;
    font-style: normal;
    color: #00ff88;
  }

  .stonk-extra {
    font-family: 'Poppins', sans-serif;
    font-size: 1.1rem;
  }

  .actions button:nth-child(1) {
    background-color: #00c267;
    box-shadow: 0 0 10px 2px rgba(0, 255, 0, 0.7);
    transition: all 0.3s ease;
  }

  .actions button:nth-child(1):hover {
    background-color: rgb(0, 146, 61);
  }

  .actions button:nth-child(2) {
    background-color: #ff0000;
    box-shadow: 0 0 10px 2px rgba(255, 0, 0, 0.7);
    transition: all 0.3s ease;
  }

  .actions button:nth-child(2):hover {
    background-color: rgb(187, 0, 0);
  }

  .invest-actions {
    color: white;
    border: none;
    font-size: 3rem;
    padding: 0.6rem 2rem;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: box-shadow 0.3s ease;
    margin: 1rem 1rem;
    font-family: 'Noto Sans TC', sans-serif;
    font-optical-sizing: auto;
    font-weight: bold;
    font-style: normal;
  }

  /* center sparkline horizontally and vertically */
  .sparkline {
    padding-left: 3px;
    padding-right: 3px;
    display: flex;
    align-items: flex-end;
    height: 60px;
    gap: 4px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    overflow-x: auto;
    padding-bottom: 4px;
  }

  .sparkline::-webkit-scrollbar {
    height: 6px;
  }
  .sparkline::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.3);
    border-radius: 3px;
  }

  .spark-bar {
    flex: 0 0 auto;
    width: 12px;
    background: gray;
    transition: height 0.2s ease;
    border-radius: 2px;
  }

  .spark-bar.up {
    background: #00ff88;
    height: 100%;
  }

  .spark-bar.down {
    background: red;
    height: 30%;
  }
</style>
