<script>
    import TitleBar from "./TitleBar.svelte"

    export let config = "";
    config = config;

</script>

<div class="h-full w-full relative p-8">

    <TitleBar text="Landmark List" on:close/>

</div>