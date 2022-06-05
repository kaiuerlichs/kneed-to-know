<script>
    import TitleBar from "./TitleBar.svelte"

    export let config = "";
    config = config;

</script>

<div class="h-full w-full relative p-8">

    <TitleBar text="Learn the Examination" on:close/>
    <p>
        <strong>Note:</strong> This mode is not implemented yet.<br/><br/>
    </p>
    <p>
        In the “Learn the examination” mode, the user will be presented with the 3D model in AR alongside a walkthrough of the knee joint examination. The examination steps will be based on the “Look – Feel – Move” paradigm and prompt the learner with self-study questions to provide a more interactive experience, making this mode useful to both independent and peer/near-peer learning.<br/><br/>
    </p>
    <p>
        As the learner progresses through the examination, various relevant landmarks will be highlighted on the model for each step, ensuring that the learner will be able to correctly identify the landmarks while examining.
    </p>

</div>