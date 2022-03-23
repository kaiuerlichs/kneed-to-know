<script>
    import TitleBar from "./TitleBar.svelte"

    import { fade, blur } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let config = "";
    config = config;

    let ready = false;

    let showLayersMenu = false;
    let layerSkinActive = true;
    let layerBoneActive = true;
    let layerTendActive = true;

    let currentLandmark = "";
    let layerType = "";
    let showLandmarkPopup = false;

    function closeView(){
        dispatch("close")
    }

    function sendSignal(sig){
        let target = document.getElementById("sceneFrame").contentWindow
        target.postMessage(sig, window.origin)
    }

    function closePopup(){
        showLandmarkPopup = false;
        currentLandmark = ""
        sendSignal("landmarks;reset")
    }

    window.addEventListener("nodesReady", () => {
        ready = true;
    })

    window.addEventListener("message", (param) => {
        let message = param.data.split(";")
        fetch("/med_data/landmarks.json")
        .then(response => response.text())
        .then((data) => {
            let landmarks = JSON.parse(data)

            let skin = landmarks.layers.skin 
            skin.forEach(el => {
                if(el.id == message[2]){
                    currentLandmark = el.name
                    layerType = "skin"
                }
            })
            let bone = landmarks.layers.bone 
            bone.forEach(el => {
                if(el.id == message[2]){
                    currentLandmark = el.name
                    layerType = "bone"
                }
            })
            let tendon = landmarks.layers.tendon
            tendon.forEach(el => {
                if(el.id == message[2]){
                    currentLandmark = el.name
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
    {#if !ready}
        <div class="absolute h-full w-full flex items-center justify-center" transition:fade>
            <div class="backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5">
                <span>Please wait for the components to initialise...</span>
            </div>
        </div>
    {/if}

    <iframe
        id="sceneFrame"
        src="./scene.html"
        title="AR Scene"
        frameborder="0"
        class="absolute h-full w-full"
    />

    {#if ready}
        <div class="absolute top-10 right-10 backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20" on:click={closeView}>
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
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            <div on:click={() => {showLayersMenu = showLayersMenu ? false : true;}}>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                </svg>
            </div>
        </div>
    {/if}

    {#if showLayersMenu}
        <div class="absolute w-full lg:w-5/12 h-full z-40 flex flex-col" transition:fade>
            <div class="m-10 h-full p-10 bg-white rounded-[20px] drop-shadow-lg">
                <TitleBar text="Controls" on:close={() => {showLayersMenu=false;}} />
                <h1 class="heading text-4xl">Layers</h1>
                <button on:click={() => {sendSignal("layer;skin;show");}}>Show Skin</button><br/>
                <button on:click={() => {sendSignal("layer;skin;hide");}}>Hide Skin</button><br/>
                <button on:click={() => {sendSignal("layer;bone;show");}}>Show Bone</button><br/>
                <button on:click={() => {sendSignal("layer;bone;hide");}}>Hide Bone</button><br/>
                <button on:click={() => {sendSignal("layer;tendon;show");}}>Show Tendon</button><br/>
                <button on:click={() => {sendSignal("layer;tendon;hide");}}>Hide Tendon</button>
            </div>
        </div>
    {/if}

    {#if showLandmarkPopup}
        <div class="invisible lg:visible">
            <div class="absolute bottom-10 left-10 flex flex-row backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5 align-middle w-1/3">
                <div class="backdrop-blur-sm bg-[#D2FCAC] text-black rounded-[20px] z-20 clickable my-auto">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                </div>
                <span class="text-xl mx-5 my-auto">
                    {currentLandmark}
                </span>
                <div class="text-white bg-white/30 rounded-[12px] z-20 clickable my-auto ml-auto justify-self-end" on:click={closePopup}>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
                    </svg>
                </div>
            </div>
        </div>
        <div class="visible lg:invisible">
            <div class="w-3/4 h-full mx-auto">
                <div class="fixed bottom-32 flex flex-row backdrop-blur-sm bg-white/30 text-white rounded-[20px] z-20 p-5 align-middle w-3/4 mx-auto">
                    <div class="backdrop-blur-sm bg-[#D2FCAC] text-black rounded-[12px] z-20 clickable my-auto">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 m-2" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                          </svg>
                    </div>
                    <span class="text-lg mx-5 my-auto">
                        {currentLandmark}
                    </span>
                    <div class="text-white rounded-[12px] bg-white/30 z-20 clickable my-auto ml-auto justify-self-end" on:click={closePopup}>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-2" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
                        </svg>
                    </div>
                </div>
            </div>
        </div>
    {/if}
</div>
