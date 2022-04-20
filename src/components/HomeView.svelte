<script>

    import LargeButton from "./LargeButton.svelte"

    export let config = "";
    config = config;

</script>

<div class="flex flex-col justify-between h-full w-full relative px-8">

    <!-- Header area -->
    <div class="w-full text-center py-20">
        <span class="heading text-5xl">Kneed To Know</span>
    </div>

    <div class="grid justify-items-stretch grid-cols-2 lg:grid-cols-3 gap-4 mb-auto">
        <div>
            <LargeButton text="Inspect the joint" dest="inspectModel" colourB="#D81159" colourA="#8F2D56" on:transition/>
        </div>
        <div>
            <LargeButton text="Learn the examination" dest="examModel" colourA="#006BA6" colourB="#0496FF" on:transition/>
        </div>
        <div>
            <LargeButton text="Co-op experience" dest="coopModel" colourB="#FF9B71" colourA="#F56960" on:transition/>
        </div>
        <div>
            <LargeButton text="List of landmarks" dest="landmarksList" colourA="#4A7856" colourB="#94FBAB" on:transition/>
        </div>
        <div>
            <LargeButton text="Examination outline" dest="examOutline" colourB="#08BDBD " colourA="#5296A5" on:transition/>
        </div>
        <div>
            <LargeButton text="About this app" dest="about" colourB="#9C7CA5" colourA="#896279" on:transition/>
        </div>
    </div>

    <div class="py-2 mt-20 flex items-center justify-center heading text-lg">
        <span>Made with</span>
        <svg xmlns="http://www.w3.org/2000/svg" class="mx-2 h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
        </svg>
        <span>at University of Dundee</span>
    </div>

</div>