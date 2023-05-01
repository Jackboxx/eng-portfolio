<script>
	import Typewriter from '../components/typewriter.svelte';
</script>

<div class="p-4 text-3xl">
<Typewriter>
    <div>
		some text to test this effect
		<div>
			<span class="text-red-400">stuff</span>
            hi
			<span class="text-green-400">more stuff</span>
		</div>
        more
        <div class="font-bold">
            <span> hello world</span>
        </div>
	</div>
</Typewriter>

<Typewriter typingDelayMs={100}>
    <div>
		some text to test this effect
		<div>
			<span class="text-red-400">stuff</span>
            hi
			<span class="text-green-400">more stuff</span>
		</div>
        more
        <div class="font-bold">
            <span> hello world</span>
        </div>
	</div>
</Typewriter>

<Typewriter typingDelayMs={20}>
    <div>
		some text to test this effect
		<div>
			<span class="text-red-400">stuff</span>
            hi
			<span class="text-green-400">more stuff</span>
		</div>
        more
        <div class="font-bold">
            <span> hello world</span>
        </div>
	</div>
</Typewriter>
</div>
