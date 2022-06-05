<script>
	import statefulSwap from "./statefulSwap"
	import HomeView from "./components/HomeView.svelte";
	import InspectModel from "./components/InspectModel.svelte";
	import ExamModel from "./components/ExamModel.svelte"
	import CoopModel from "./components/CoopModel.svelte"
	import LandmarkList from "./components/LandmarkList.svelte"
	import Tutorial from "./components/Tutorial.svelte";
	import AboutView from "./components/AboutView.svelte";
	
	import {fade} from "svelte/transition"
	const {onOutro, transitionTo, state} = statefulSwap("main")

	function evtTransitionTo(event){
		transitionTo(event.detail.state)
	}
</script>

<div class="h-screen flex">
	{#if $state == "main"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<HomeView on:transition={evtTransitionTo}/>
		</div>
	{:else if $state == "inspectModel"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<InspectModel on:close={() => transitionTo("main")}/>
		</div>
	{:else if $state == "examModel"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<ExamModel on:close={() => transitionTo("main")}/>
		</div>
	{:else if $state == "coopModel"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<CoopModel on:close={() => transitionTo("main")}/>
		</div>
	{:else if $state == "landmarksList"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<LandmarkList on:close={() => transitionTo("main")}/>
		</div>
	{:else if $state == "tutorial"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<Tutorial on:close={() => transitionTo("main")}/>
		</div>
	{:else if $state == "about"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<AboutView on:close={() => transitionTo("main")}/>
		</div>
	{/if}
</div>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Amatic+SC:wght@400;700&display=swap" rel="stylesheet">

<style global lang="postcss">
	@tailwind base;
	@tailwind components;
	@tailwind utilities;

	.heading {
		font-family: "Amatic SC", sans-serif;
		font-weight: bold;
	}

	.backdrop-blur {
  		backdrop-filter: blur(8px);
	}
	.backdrop-blur-sm {
  		backdrop-filter: blur(4px);
	}
	.backdrop-blur-md {
  		backdrop-filter: blur(12px);
	}
	.inset-center {
		position: absolute;
		left: 50%;
		transform: translateX(-50%);
	}
</style>
