<script>
    import TitleBar from "./TitleBar.svelte"
    import { slide } from 'svelte/transition';

    export let config = "";
    config = config;

    // Load landmarks data
    let landmarks = ""
    let landmarkArr = []
    fetch("/med_data/landmarks.json")
    .then(response => response.text())
    .then((data) => {
        landmarks = JSON.parse(data)
        
        Object.entries(landmarks.layers).forEach(([key, value]) => {
            for(let landmark of value){
                landmarkArr.push(landmark)
                landmarkArr = landmarkArr
            }
        })

        landmarkArr.sort((a, b) => a.name.localeCompare(b.name))

        landmarkArr = landmarkArr.map(v => ({...v, isDisplayed: false}))

        console.log(landmarkArr)
    })

</script>

<div class="h-full w-full relative p-8">

    <TitleBar text="List of landmarks" on:close/>

            {#each landmarkArr as landmark}
                <div class="mb-4">
                    <h1 class="cursor-pointer text-lg py-1" on:click={() => {landmark.isDisplayed = !landmark.isDisplayed;}}>
                        {landmark.name}
                        {#if landmark.isDisplayed}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-[1.125rem] translate-y-[-0.125rem] inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M5 15l7-7 7 7" />
                        </svg>
                        {:else}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-[1.125rem] translate-y-[-0.125rem] inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
                        </svg>
                        {/if}
                    </h1>
                    {#if landmark.isDisplayed}
                        <div transition:slide>
                            {#each landmark.desc as paragraph}
                                <p>{paragraph}</p>
                            {/each}
                        </div>
                    {/if}
                </div>
            {/each}

</div>