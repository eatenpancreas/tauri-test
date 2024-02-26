<script lang="ts">
    import type {CoinAmount} from "$lib/Coin";

    export let coin: CoinAmount;
    export let className = "";
    export let click: () => void = () => {};
</script>

<div class={className} on:click={click}>
    <slot/>
    
    {#if coin === 0.01}
        <img src="coins/000-01eu.png" alt="1 Eurocent">
    {:else if coin === 0.02}
        <img src="coins/000-02eu.png" alt="2 Eurocent">
    {:else if coin === 0.05}
        <img src="coins/000-05eu.png" alt="5 Eurocent">
    {:else if coin === 0.10}
        <img src="coins/000-10eu.png" alt="10 Eurocent">
    {:else if coin === 0.20}
        <img src="coins/000-20eu.png" alt="20 Eurocent">
    {:else if coin === 0.50}
        <img src="coins/000-50eu.png" alt="50 Eurocent">
    {:else if coin === 1}
        <img src="coins/001-00eu.png" alt="1 Euro">
    {:else if coin === 2}
        <img src="coins/002-00eu.png" alt="2 Euro">
    {:else if coin === 5}
        <img src="coins/005-00eu.png" alt="5 Euro">
    {:else if coin === 10}
        <img src="coins/010-00eu.png" alt="10 Euro">
    {:else if coin === 20}
        <img src="coins/020-00eu.png" alt="20 Euro">
    {:else if coin === 50}
        <img src="coins/050-00eu.png" alt="50 Euro">
    {:else if coin === 100}
        <img src="coins/100-00eu.png" alt="100 Euro">
    {:else if coin === 200}
        <img src="coins/200-00eu.png" alt="200 Euro">
    {:else if coin === 500}
        <img src="coins/500-00eu.png" alt="500 Euro">
    {/if}
</div>