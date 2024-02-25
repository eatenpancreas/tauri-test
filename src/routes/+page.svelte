<script>
    let message = $state("I love Tauri + Svelte")
    
    function click() {
        message += " + Svelte";
    }
</script>

<button class="border-black border bg-gray-300 p-2" on:click={click}>Press me.</button>

<h1 class="text-2xl font-bold">Welcome to SvelteKit!</h1>
<h2 class="text-blue-800">{message}</h2>
<p>Visit <a class="text-blue-300 border-b border-blue-300" href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
