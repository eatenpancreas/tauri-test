<script lang="ts">
    import Coin from "$lib/Coin.svelte";
    import type {CoinAmount} from "$lib/Coin";

    const coins: [0.01, 0.02, 0.05, 0.10, 0.20, 0.50, 1, 2, 5, 10, 20, 100, 200, 500] 
        = [0.01, 0.02, 0.05, 0.10, 0.20, 0.50, 1, 2, 5, 10, 20, 100, 200, 500]
    
    let selected: CoinAmount | undefined = $state();
    let inventory: { ty: CoinAmount, count: number }[] = $state(coins.map(x => {return { ty: x, count: 0}}));
    let selectedAmount = $derived(inventory.find(x => x.ty == selected)?.count);
    let totalCount = $derived(inventory.reduce((acc, x) => acc + x.count, 0));
    let totalAmount = $derived(inventory.reduce((acc, x) => acc + x.ty * x.count, 0));
    
    function incDec(increase: boolean) {
        const i = inventory.findIndex(x => x.ty === selected);
        if (i >= 0) {
            if (increase) inventory[i].count += 1;
            else if (inventory[i].count > 0) inventory[i].count -= 1;
        }
    }

    function setTo(val: string) {
        const i = inventory.findIndex(x => x.ty === selected);
        if (i >= 0) {
            inventory[i].count = parseFloat(val);
        }
    }
</script>

<div class="flex items-center gap-5 p-5 overflow-x-scroll">
    {#each coins as coin, index}
        <Coin coin={coin} click={() => {if (selected !== coin) selected = coin; else selected = undefined} }
              className={"relative min-w-28 w-40 transition hover:border-black/20 hover:border p-2 rounded-xl " 
              + (selected === coin? "border border-black" : "")}
        >
            <div class="absolute">{inventory[index]?.count ?? 0}</div>
        </Coin>
    {/each}
</div>

<div class="flex w-full justify-center my-16">
    {#if selected !== undefined}
        <div class="w-48">
            <button class="transition flex justify-between w-full items-center p-4
            text-green-600 border border-black text-8xl rounded-xl hover:bg-green-200 mb-10"
            on:click={() => incDec(true)}>
                <span class="block pb-3">+</span> <Coin className="w-20" coin={selected}/>
            </button>
            <input type="number" value={selectedAmount} class="bg-transparent border border-black p-4 rounded-xl w-48 mb-10"
                   on:focusout={(e) => setTo(e.target?.value)} 
                   on:keydown={(e) => { if (e.key === "Enter") setTo(e.target.value); }}
            >
            <button class="transition flex justify-between w-full items-center p-4
            text-red-600 border border-black text-8xl rounded-xl hover:bg-red-200"
            on:click={() => incDec(false)}>
                <span class="block pb-3">-</span> <Coin className="w-20" coin={selected}/>
            </button>
        </div>
    {/if}
</div>

<div class="flex flex-col items-center">
    <h1 class="text-3xl p-2 font-bold">Totaal aantal munten geteld: {totalCount}</h1>
    <h1 class="text-3xl p-2 font-bold">Totaal: €{new Intl.NumberFormat('en-DE').format(totalAmount)}</h1>
</div>