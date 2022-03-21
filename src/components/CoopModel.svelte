<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    function closeView(){
        dispatch("close")
    }

    export let config = "";
    config = config;

</script>

<div class="flex align-items-center place-content-center h-full w-full relative px-8">

    <span class="text-xl">
        Coop Model
    </span>

</div>