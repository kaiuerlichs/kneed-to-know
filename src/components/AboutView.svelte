<script>
    import TitleBar from "./TitleBar.svelte"

    export let config = "";
    config = config;

</script>

<div class="h-full w-full relative">

    <div class="m-8">
        <TitleBar text="About this app" on:close/>
    </div>

    <div class="w-full text-right p-4 my-8">
        <span class="heading text-4xl">developed @ university of dundee</span><br/>
        <span class="heading text-8xl">virtual anatomy project 2022</span>
    </div>
    <div class="w-full my-4">
        <div class="grid lg:grid-cols-3 w-full lg:justify-items-center">
            <div class="p-4 w-full bg-[#F08CAE]">
                <h1 class="heading text-4xl text-center py-2">Team Anatomy</h1>
                <div class="grid grid-cols-2 items-center py-4">
                    <div class="w-full">
                        <img class="rounded-full mx-auto h-24 drop-shadow-lg" src="https://picsum.photos/id/1011/200/200" alt="">
                        <h1 class="heading text-2xl pt-2 text-center">Wan Nee Shue</h1>
                    </div>
                    <div class="w-full">
                        <img class="rounded-full mx-auto h-24 drop-shadow-lg" src="https://picsum.photos/id/1004/200/200" alt="">
                        <h1 class="heading text-2xl pt-2 text-center">Celine Shaoyan Wang</h1>
                    </div>
                </div>
                <p class="text-lg pt-2">
                    Our brilliant medical and anatomy students make sure you actually learn something. They collate the information displayed in the application, and further advise the other teams on what exactly is needed in anatomical education.
                </p>
            </div>
            <div class="p-4 w-full bg-[#96C9DC]">
                <h1 class="heading text-4xl text-center py-2">Team Artists</h1>
                <div class="grid grid-cols-3 items-center py-4">
                    <div class="w-full">
                        <img class="rounded-full mx-auto h-24 drop-shadow-lg" src="https://picsum.photos/id/1025/200/200" alt="">
                        <h1 class="heading text-2xl pt-2 text-center">Sofia Nahman</h1>
                    </div>
                    <div class="w-full">
                        <img class="rounded-full mx-auto h-24 drop-shadow-lg" src="https://picsum.photos/id/1044/200/200" alt="">
                        <h1 class="heading text-2xl pt-2 text-center">Ruby Mengtian Lu</h1>
                    </div>
                    <div class="w-full">
                        <img class="rounded-full mx-auto h-24 drop-shadow-lg" src="https://picsum.photos/id/1062/200/200" alt="">
                        <h1 class="heading text-2xl pt-2 text-center">Kelly Clayton</h1>
                    </div>
                </div>
                <p class="text-lg py-2">
                    Team Artists created that knee you were just looking at! They reconstructed a 3D model from CT-scan data of the skeleton and skin, built the ligaments and tendons and made it look pretty and snappy!
                </p>
            </div>
            <div class="p-4 w-full bg-[#D2FCAC]">
                <h1 class="heading text-4xl text-center py-2">Team Coders</h1>
                <div class="grid grid-cols-1 items-center py-4">
                    <div class="w-full">
                        <img class="rounded-full mx-auto h-24 drop-shadow-lg" src="https://picsum.photos/id/1042/200/200" alt="">
                        <h1 class="heading text-2xl pt-2 text-center">Kai Uerlichs</h1>
                    </div>
                </div>
                <p class="text-lg pt-2">
                    Our coding team is responsible for putting this web app together. With the magic of HTML, JavaScript and AR technologies, they make the knee show up right in front of you!
                </p>
            </div>
        </div>
    </div>
    <div class="w-full p-4 place-items-center">
        <h1 class="heading text-4xl text-center py-2">About the project</h1>
        <div class="lg:w-1/2 mx-auto my-4">
            <p class="text-lg">
                This application was developed as part of the Virtual Anatomy Project 2022 at the University of Dundee. Its aim is for interdisciplinary development of digital tools in the field of anatomy and medicine, with an emphasis on augmented and virtual reality implementations. The main target of the Virtual Anatomy Project 2022 was web-based AR.  
            </p>
            <p class="text-lg mt-2">
                Our application aims to facilitate peer and near-peer learning in medical and anatomical education. In particular, the application makes use of various Augmented Reality (AR) technologies to create an interactive environment in which medical students can learn about the examination of the knee joint in a fun and engaging manner.
            </p>
        </div>
    </div>

</div>