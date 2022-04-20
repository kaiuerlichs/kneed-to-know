<script>
    // Import title bar component and svelte dependencies
    import TitleBar from "./TitleBar.svelte"
    import { fade, blur } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    // Component config
    export let config = "";
    config = config;

    // AR ready guard
    let ready = false;

    // Layer activity variables
    let showLayersMenu = false;
    let layerSkinActive = true;
    let layerBoneActive = true;
    let layerTendActive = true;
    let showLandmarks = true;

    $: {
        if(ready){
            if(layerSkinActive){
                sendSignal("layer;skin;show");
            }
            else{
                sendSignal("layer;skin;hide");
            }

            if(layerBoneActive){
                sendSignal("layer;bone;show");
            }
            else{
                sendSignal("layer;bone;hide");
            }

            if(layerTendActive){
                sendSignal("layer;tendon;show");
            }
            else{
                sendSignal("layer;tendon;hide");
            }
        }
    }

    // Landmark popup variables
    let currentLandmark = "";
    let landmarkDesc = "";
    let layerType = "";
    let showLandmarkPopup = false;
    let showLandmarkInfo = false;

    // Function to dispatch close event
    function closeView(){
        dispatch("close")
    }

    function toggleLandmarks(){
        if(showLandmarks){
            showLandmarks = false;
            sendSignal("landmark;hide");
        }
        else{
            showLandmarks = true;
            sendSignal("landmark;show");
        }
    }

    // Function to send signal to AR frame
    function sendSignal(sig){
        let target = document.getElementById("sceneFrame").contentWindow
        target.postMessage(sig, window.origin)
    }

    // Function to dismiss popup
    function closePopup(){
        showLandmarkPopup = false;
        sendSignal("landmark;reset")
    }

    // Function to handle ready event from AR scene
    window.addEventListener("nodesReady", () => {
        ready = true;
    })

    // Function to handle signal from AR frame
    window.addEventListener("message", (param) => {
        // Find correct landmark in json database
        let message = param.data.split(";")
        fetch("/med_data/landmarks.json")
        .then(response => response.text())
        .then((data) => {
            let landmarks = JSON.parse(data)

            let skin = landmarks.layers.skin 
            skin.forEach(el => {
                if(el.id == message[2]){
                    currentLandmark = el.name
                    landmarkDesc = el.desc
                    layerType = "skin"
                }
            })
            let bone = landmarks.layers.bone 
            bone.forEach(el => {
                if(el.id == message[2]){
                    currentLandmark = el.name
                    landmarkDesc = el.desc
                    layerType = "bone"
                }
            })
            let tendon = landmarks.layers.tendon
            tendon.forEach(el => {
                if(el.id == message[2]){
                    currentLandmark = el.name
                    landmarkDesc = el.desc
                    layerType = "tendon"
                }
            })

            if(currentLandmark != ""){
                showLandmarkPopup = true;
            }
        })
    })
</script>

<div class="h-full w-full relative bg-black">

    <!-- Display laoding message while AR scene is initialising -->
    {#if !ready}
        <div class="absolute h-full w-full flex items-center justify-center" transition:fade>
            <div class="backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5">
                <span>Please wait for the components to initialise...</span>
            </div>
        </div>
    {/if}

    <!-- Embed AR scene as iframe -->
    <iframe
        id="sceneFrame"
        src="./scene.html"
        title="AR Scene"
        frameborder="0"
        class="absolute h-full w-full"
    />

    <!-- Insert DOM overlay -->
    {#if ready}
        <div class="cursor-pointer absolute top-10 right-10 backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20" on:click={closeView}>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
            </svg>
        </div>
        <div class="absolute bottom-10 inset-center align-middle backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 grid grid-cols-3">
            <div>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
            </div>
            <div on:click={toggleLandmarks}>
                {#if showLandmarks}
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                    </svg>
                {:else}
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
                    </svg>
                {/if}
            </div>
            <div on:click={() => {showLayersMenu = showLayersMenu ? false : true;}} class="cursor-pointer">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                </svg>
            </div>
        </div>
    {/if}

    <!-- Layers menu code -->
    {#if showLayersMenu}
        <div class="absolute w-full lg:w-5/12 h-full z-40 flex flex-col" transition:fade>
            <div class="m-10 h-full p-10 bg-white rounded-[20px] drop-shadow-lg">
                <TitleBar text="Controls" on:close={() => {showLayersMenu=false;}} />
                <h1 class="heading text-4xl">Toggle Layers</h1>
                <label>
                    <input type="checkbox" bind:checked={layerSkinActive}>
                    Skin
                </label>
                <br>
                <label>
                    <input type="checkbox" bind:checked={layerBoneActive}>
                    Bone
                </label>
                <br>
                <label>
                    <input type="checkbox" bind:checked={layerTendActive}>
                    Tendons and Ligaments
                </label>
            </div>
        </div>
    {/if}

    <!-- Landmark info code -->
    {#if showLandmarkInfo}
        <div class="absolute w-full lg:w-5/12 h-full z-40 flex flex-col" transition:fade>
            <div class="m-10 h-full p-10 bg-white rounded-[20px] drop-shadow-lg">
                <TitleBar text={currentLandmark} on:close={() => {showLandmarkInfo=false;}} />
                <p>
                    {landmarkDesc}
                </p>
            </div>
        </div>
    {/if}

    <!-- Landmark Popup code -->
    {#if showLandmarkPopup}
        <div class="invisible lg:visible" transition:fade>
            <div class="absolute bottom-10 left-10 flex flex-row backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5 align-middle w-1/3" on:click={() => {showLandmarkInfo=true;}}>
                <div class="backdrop-blur-sm bg-[#D2FCAC] text-black rounded-[20px] z-20 cursor-pointer my-auto">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                </div>
                <span class="text-xl mx-5 my-auto">
                    {currentLandmark}
                </span>
                <div class="text-white bg-white/30 rounded-[12px] z-30 cursor-pointer my-auto ml-auto justify-self-end" on:click|stopPropagation={closePopup}>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
                    </svg>
                </div>
            </div>
        </div>
        <div class="visible lg:invisible" transition:fade>
            <div class="w-3/4 h-full mx-auto">
                <div class="fixed bottom-32 flex flex-row backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5 align-middle w-3/4 mx-auto" on:click={() => {showLandmarkInfo=true;}}>
                    <div class="backdrop-blur-sm bg-[#D2FCAC] text-black rounded-[12px] z-20 cursor-pointer my-auto">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 m-2" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                          </svg>
                    </div>
                    <span class="text-lg mx-5 my-auto">
                        {currentLandmark}
                    </span>
                    <div class="text-white rounded-[12px] bg-white/30 z-30 cursor-pointer my-auto ml-auto justify-self-end" on:click|stopPropagation={closePopup}>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-2" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
                        </svg>
                    </div>
                </div>
            </div>
        </div>
    {/if}
</div>
