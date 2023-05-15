<script lang="ts">
	import Typewriter from './typewriter.svelte';

	let speed = 140;
	let skipTyping = false;
</script>

<div
	class="overflow-hidde text-md relative
   min-h-screen bg-black p-4 font-mono text-white subpixel-antialiased"
>
	<div class="sticky top-4 flex justify-between">
		<a class="cursor-pointer" href="/">⇦ Back</a>
		<input type="range" min="10" max="160" bind:value={speed} />
	</div>

	<div class="crt-screen h-full">
		<Typewriter typingDelayMs={160 - speed} {skipTyping}>
			<slot />
		</Typewriter>
	</div>
</div>

<style>
	:global(ul) {
		list-style: none;
	}
	:global(ul > li) {
		margin-left: 12px;
		margin-bottom: 8px;
	}

	input[type='range'] {
		-webkit-appearance: none;
		appearance: none;
		width: 40%;
		cursor: pointer;
		outline: none;
		overflow: hidden;
		border-radius: 16px;
	}

	/* Track: webkit browsers */
	input[type='range']::-webkit-slider-runnable-track {
		height: 16px;
		background: #fff;
		border-radius: 16px;
	}

	/* Track: Mozilla Firefox */
	input[type='range']::-moz-range-track {
		height: 16px;
		background: #fff;
		border-radius: 16px;
	}

	/* Thumb: webkit */
	input[type='range']::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		height: 15px;
		width: 15px;
		background-color: #fff;
		border-radius: 50%;
		border: 2px solid #28b0ff;
		box-shadow: -407px 0 0 400px #28b0ff;
	}

	/* Thumb: Firefox */
	input[type='range']::-moz-range-thumb {
		height: 15px;
		width: 15px;
		background-color: #fff;
		border-radius: 50%;
		border: 2px solid #28b0ff;
		box-shadow: -407px 0 0 400px #28b0ff;
	}
</style>
