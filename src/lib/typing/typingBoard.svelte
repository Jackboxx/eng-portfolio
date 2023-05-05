<script lang="ts">
	import Button from '../utils/button.svelte';
	import Slider from '../utils/slider.svelte';
	import Typewriter from './typewriter.svelte';

	let speed = 100;
	let skipTyping = false;
</script>

<div
	class="coding inverse-toggle overflow-hidde relative h-full rounded-lg bg-gray-800 px-5 pb-6 pt-4 font-mono
              text-sm leading-normal text-gray-100 subpixel-antialiased shadow-lg"
>
	<div class="top mb-2 flex">
		<div class="h-3 w-3 rounded-full bg-red-500" />
		<div class="ml-2 h-3 w-3 rounded-full bg-orange-300" />
		<div class="ml-2 h-3 w-3 rounded-full bg-green-500" />
	</div>
	<div class="absolute bottom-0 right-0 w-[20%] min-w-[300px] p-4">
		<Slider name={''} bind:value={speed} min={10} max={150} />
		<div class="mt-4">
			<Button onClick={() => (skipTyping = true)}>Skip</Button>
		</div>
	</div>
	<div class="w-[50%]">
		<Typewriter typingDelayMs={160 - speed} {skipTyping}>
			<slot />
		</Typewriter>
	</div>
</div>

<style>
</style>
