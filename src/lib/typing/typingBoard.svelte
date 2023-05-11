<script lang="ts">
	import Typewriter from './typewriter.svelte';

	let speed = 100;
	let skipTyping = false;
</script>

<div
	class="overflow-hidde text-md relative h-screen
   bg-black p-4
              font-mono text-white subpixel-antialiased"
>
	<div class="crt-screen h-full">
		<Typewriter typingDelayMs={160 - speed} {skipTyping}>
			<slot />
		</Typewriter>
	</div>
</div>
