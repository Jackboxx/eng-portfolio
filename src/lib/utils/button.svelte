<script lang="ts">
	export let onClick: () => void;
</script>

<div
	class="flex w-full items-center justify-center rounded-xl border-2 border-solid
    border-transparent bg-purple-600 p-2 text-2xl font-bold text-white duration-150
    hover:border-purple-600 hover:bg-white hover:text-purple-600"
	on:click={onClick}
	on:keydown={null}
>
	<slot />
</div>
