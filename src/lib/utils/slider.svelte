<script lang="ts">
	export let min = 0;
	export let max = 100;
	export let name = '';

	export let value = (min + max) / 2;
</script>

<div class="flex w-full justify-start gap-2">
	<label class="flex-grow-0" for="range">{name}</label>
	<input class="flex-grow" bind:value type="range" {min} {max} id="range" />
</div>
