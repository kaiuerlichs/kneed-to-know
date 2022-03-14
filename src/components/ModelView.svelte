<script>
    import { createEventDispatcher } from 'svelte';
    import { fade } from 'svelte/transition';
    const dispatch = createEventDispatcher();

    export let config = "";
    config = config;

    let ready = false;

    function clickHandler(){
        dispatch("closeModelView")
    }

    window.addEventListener("nodesReady", () => {
        ready = true;
    })
</script>

<div class="h-full w-full relative bg-black">
    {#if !ready}
        <div class="absolute h-full w-full flex items-center justify-center" transition:fade>
            <div class="backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5">
                <span>Please wait for the components to initialise...</span>
            </div>
        </div>
    {/if}

    <iframe
        src="./scene.html"
        title="AR Scene"
        frameborder="0"
        class="absolute h-full w-full"
    />

    {#if ready}
        <div class="absolute top-10 right-10 backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20" on:click={clickHandler} transition:fade>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
            </svg>
        </div>
        <div class="absolute bottom-10 inset-center align-middle backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 grid grid-cols-3" transition:fade>
            <div>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
            </div>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            <div>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                </svg>
            </div>
        </div>
    {/if}
</div>
