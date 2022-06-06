<script>
    import TitleBar from "./TitleBar.svelte"

    export let config = "";
    config = config;

</script>

<div class="h-full w-full relative p-8">

    <TitleBar text="Co-op experience" on:close/>
    <p>
        <strong>Note:</strong> This mode is not implemented yet.<br/><br/>
    </p>
    <p>
        The “co-op” experience will connect two or more user devices with each other, using a secure peer-to-peer connection. When connected, the users will all be presented with the model in the same state across their devices. In discussion of the anatomical model, users will be able to create virtual pointers at parts of the model, and all transformations to the model (resizing, rotation and showing/hiding of layers) will be reflected on all devices. 
    </p>

</div>