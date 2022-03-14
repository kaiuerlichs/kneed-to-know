<script>
	import statefulSwap from "./statefulSwap"
	import ModelView from "./components/ModelView.svelte";
	import {fade} from "svelte/transition"
	const {onOutro, transitionTo, state} = statefulSwap("main")
</script>

<div class="h-screen flex justify-center items-center">

	{#if $state == "main"}
		<button class="p-3 bg-slate-800 text-white font-mono shadow-md" on:click={() => transitionTo("model")} on:outroend={onOutro} transition:fade>
			Launch Model Viewer
		</button>
	{:else if $state == "model"}
		<div class="h-full w-full" on:outroend={onOutro} transition:fade>
			<ModelView on:closeModelView={() => transitionTo("main")}/>
		</div>
	{/if}
</div>

<style global lang="postcss">
	@tailwind base;
	@tailwind components;
	@tailwind utilities;

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
