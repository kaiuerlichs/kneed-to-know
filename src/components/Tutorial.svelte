<script>
    import TitleBar from "./TitleBar.svelte"

    export let config = "";
    config = config;

</script>

<div class="h-full w-full relative p-8">

    <TitleBar text="Tutorial and resources" on:close/>

    <div class="h-full w-full relative">

        <div class="w-full p-4 place-items-center">
            <div class="lg:w-1/2 mx-auto my-4">
                <h1 class="heading text-4xl py-2">Getting started</h1>
                <p class="text-lg mb-2">
                    To get started, make sure your device meets the system requirements and download the <strong>Hiro marker</strong> below. It is recommended to print the marker onto thick paper to achieve the most consistent and hassle-free Augmented Reality experience, but as long as the marker is clearly visible, the application should work. It might also be useful to leave a white border around the marker if you intend to place it on a dark surface.  
                </p>
                <p class="text-lg mb-2">
                    To launch the AR experience, navigate to the home screen of the application and press "Inspect the model", which will load the general-purpose model viewer. Wait until the application is fully initialised and, if prompted, allow the application to use your device's camera. Now, point your device's camera at the marker, and the knee joint model should appear levitating above it. This works best in ample lighting conditions.
                </p>
            </div>
            <div class="lg:w-1/2 mx-auto my-4">
                <h1 class="heading text-4xl py-2">Using the app</h1>
                <p class="text-lg mb-2">
                    The initial model configuration will show you the skin layer of the knee. Familiarise you with the basic controls, such as <strong>pinching the screen</strong> to increase and decrease the size of model and <strong>swiping left and right</strong> to rotate it. Try moving your device around the marker, which will allow you to view to model from different angles. Remember the marker must be in view of the camera for this to work.
                </p>
                <p class="text-lg mb-2">
                    To adjust the model configuration, take a look at the control bar in the bottom centre of the screen.
                </p>
                <div class="my-5 mx-auto max-w-fit backdrop-blur-sm bg-black/30 text-white rounded-[20px] grid grid-cols-3">
                    <div >
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                        </svg>
                    </div>
                    <div>
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                            </svg>
                    </div>
                    <div>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 m-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                        </svg>
                    </div>
                </div>
                <p class="text-lg mb-2">
                    Clicking the 
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mb-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" /></svg>
                    button opens the <strong>layers menu</strong>. Here, you can toggle the skin, bone and tendon/ligament layers on and off. If you deactive the skin layer, the app will highlight important landmarks on the model using coloured orbs.
                </p>
                <p class="text-lg mb-2">
                    The
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mb-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" /></svg>
                    button toggles whether these landmarks are visible or not, so you can have a look at the model without any annotations if you wish.
                </p>
                <p class="text-lg mb-2">
                    Lastly, the 
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mb-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
                    button opens a list of all the landmarks that are placed on the model. You can select them by name here to highlight them in the AR view.
                </p>
            </div>
            <div class="lg:w-1/2 mx-auto my-4">
                <h1 class="heading text-4xl py-2">System requirements</h1>
                <p class="text-lg mb-2">
                    Good news! The browser-based AR experience should be compatible with most modern mobile devices, such as your smartphone or tablet. If you understand technical jargon, the two main dependencies are the Stream API and WebGL. If you dont, just make sure your device's browser is on these compatibility lists:
                </p>
                <p class="text-lg mb-2">
                    <a href="https://caniuse.com/webgl">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mb-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" /></svg>
                        Compatibility list for WebGL
                    </a><br/>
                    <a href="https://caniuse.com/stream">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mb-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" /></svg>
                        Compatibility list for Stream API
                    </a>
                </p>
            </div>
            <div class="lg:w-1/2 mx-auto my-4">
                <h1 class="heading text-4xl py-2">Downloads</h1>
                <p class="text-lg mb-2">
                    Click below to downlaod the Hiro marker, which is required to view the AR model.
                </p>
                <p class="text-lg mb-2">
                    <a href="/downloads/Kneed2Know-hiro-marker.png" download>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mb-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" /></svg>
                        Download Hiro marker
                    </a>
                </p>
            </div>
        </div>

    </div>

</div>