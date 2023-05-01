<script lang="ts">
	import Button from '../utils/button.svelte';
	import Slider from '../utils/slider.svelte';
	import Typewriter from './typewriter.svelte';

	let speed = 50;
	let skipTyping = false;
</script>

<div class="relative">
	<div
		class="absolute right-4 top-8 w-[20%] min-w-[300px] rounded-xl border-4 border-solid
    border-slate-500 p-4"
	>
		<Slider name={'Typewriter Speed'} bind:value={speed} min={10} max={150} />
		<div class="mx-16 mt-4">
			<Button onClick={() => (skipTyping = true)}>Skip</Button>
		</div>
	</div>
	<Typewriter typingDelayMs={speed} {skipTyping}>
		<slot />
	</Typewriter>
</div>
