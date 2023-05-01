<script context="module" lang="ts">
    function wait(delay: number) {
        return new Promise((resolve) => {
            setTimeout(resolve, delay);
        })
    }

    async function typewriteNode(element: Node, text: string, delay: number) {
        for (let i = 0; i <= text.length; i++) {
            element.nodeValue = text.substring(0, i);
            await wait(delay);
        }
    }

    async function typewriteTree(element: Node, fill: {content: string[], current:
    number}, delay: number) {
        if (element.nodeType === Node.TEXT_NODE) {
            const text = fill.content[fill.current];
            fill.current += 1;

            await typewriteNode(element, text, delay);
        }

        for (let i = 0; i < element.childNodes.length; i++) {
            const child = element.childNodes[i];
            await typewriteTree(child, fill, delay);
        }
	}

    function clearText(element: Node): string[] {
        const content: string[] = [];
        if (element.nodeType === Node.TEXT_NODE && element.nodeValue) {
            content.push(element.nodeValue.replace(/\s+/g, ' '));
            element.nodeValue = '';
        };

        for (let i = 0; i < element.childNodes.length; i++) {
            const child = element.childNodes[i];
            content.push(...clearText(child));
        }

        return content;
    }
</script>

<script lang="ts">
	import { onMount } from 'svelte';

    export let typingDelayMs = 50

	let parent: HTMLElement;
    let height: number;
    let actualHeight: number;

	onMount(async () => {
        actualHeight = height;
        console.log(actualHeight);
        const content = clearText(parent);
        await typewriteTree(parent, {content, current: 0}, typingDelayMs);
	});
</script>

<div bind:this={parent} bind:clientHeight={height} style={`height: ${actualHeight}px`}>
	<slot  />
</div>
