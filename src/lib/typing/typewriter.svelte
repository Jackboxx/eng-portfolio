<script lang="ts">
	import { onMount } from 'svelte';

	export let typingDelayMs = 50;
	export let inbetweenNodeDelayMs = 150;
	export let skipTyping = false;

	let parent: HTMLElement;
	let height: number;
	let actualHeight: number;

	onMount(async () => {
		actualHeight = height;
		if (skipTyping) return;

		const content = clearText(parent);
		await typewriteTree(parent, { content, current: 0 });
	});

	function wait(delay: number) {
		return new Promise((resolve) => {
			setTimeout(resolve, delay);
		});
	}

	async function typewriteNode(element: Node, text: string) {
		for (let i = 0; i <= text.length; i++) {
			element.nodeValue = text.substring(0, i);
			await wait(typingDelayMs);
		}
	}

	async function typewriteTree(
		element: Node,
		fill: { content: string[]; current: number },
	) {
		if (element.nodeType === Node.TEXT_NODE) {
			const text = fill.content[fill.current];
			fill.current += 1;

			await typewriteNode(element, text);
		}

		for (let i = 0; i < element.childNodes.length; i++) {
			const child = element.childNodes[i];
			await typewriteTree(child, fill);
			await wait(inbetweenNodeDelayMs);
		}
	}

	function clearText(element: Node): string[] {
		const content: string[] = [];
		if (element.nodeType === Node.TEXT_NODE && element.nodeValue) {
			content.push(element.nodeValue.replace(/\s+/g, ' '));
			element.nodeValue = '';
		}

		for (let i = 0; i < element.childNodes.length; i++) {
			const child = element.childNodes[i];
			content.push(...clearText(child));
		}

		return content;
	}
</script>

{#key skipTyping}
	<div bind:this={parent} bind:clientHeight={height} style={`height: ${actualHeight}px`}>
		<slot />
	</div>
{/key}
