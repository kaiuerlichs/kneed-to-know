<script>

    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let text;
    export let dest;
    export let colourA;
    export let colourB;

    function sendTransition(){
        dispatch("transition", { state: dest })
    }
    
</script>

<div 
    class="flex mx-auto w-full max-w-md cursor-pointer drop-shadow-md text-right h-36 rounded-3xl p-4 text-white font-bold text-lg lg:text-xl place-content-end"
    style="
        background: {colourA};
        background: linear-gradient(0deg, {colourA} 0%, {colourB} 100%);
    "
    on:click="{sendTransition}"
>
    <div class="place-self-end">{text}</div>
</div>
