<script context="module" lang="ts">
	export type TocEntry = {
		position: {
			x: number;
			y: number;
		};
		href: string;
		title: string;
	};

	function createTocEntryElement(
		parent: HTMLElement,
		title: string,
		href: string,
		position: { x: number; y: number },
		elements: HTMLElement[],
	) {
		let { x, y } = position;
		let w = 16;
		let h = 16;

		let element = document.createElement('a');

		element.href = href;
		element.style.width = `${w}px`;
		element.style.height = `${h}px`;
		element.style.left = `${x - w / 2}px`;
		element.style.top = `${y - h / 2}px`;
		element.classList.add('star-link');

		let childElement = document.createElement('div');
		childElement.innerText = title;
		childElement.classList.add('star-link-info');

		element.appendChild(childElement);
		elements.push(element);
		parent.appendChild(element);
	}

	function drawStar(
		ctx: CanvasRenderingContext2D,
		position: { x: number; y: number },
		spikes: number,
		outerRadius: number,
		innerRadius: number,
		color: string,
	) {
		let rot = (Math.PI / 2) * 3;

		let { x, y } = position;
		const originalX = x;
		const originalY = y;

		const step = Math.PI / spikes;

		ctx.strokeStyle = '#000';
		ctx.beginPath();
		ctx.moveTo(originalX, originalY - outerRadius);
		for (let i = 0; i < spikes; i++) {
			x = originalX + Math.cos(rot) * outerRadius;
			y = originalY + Math.sin(rot) * outerRadius;
			ctx.lineTo(x, y);
			rot += step;

			x = originalX + Math.cos(rot) * innerRadius;
			y = originalY + Math.sin(rot) * innerRadius;
			ctx.lineTo(x, y);
			rot += step;
		}
		ctx.lineTo(originalX, originalY - outerRadius);
		ctx.closePath();
		ctx.lineWidth = 5;
		ctx.strokeStyle = color;
		ctx.stroke();
		ctx.fillStyle = color;
		ctx.fill();
	}

	function drawToc(
		parent: HTMLElement,
		canvas: HTMLCanvasElement | undefined,
		entries: TocEntry[],
		color: string,
		hrefPrefix: string,
		elements: HTMLElement[],
	) {
		if (!canvas) return;
		const context = canvas.getContext('2d');
		if (!context) return;

		elements.forEach((e) => e.remove());

		for (let i = 0; i < entries.length; i++) {
			createTocEntryElement(
				parent,
				entries[i].title,
				hrefPrefix + entries[i].href,
				entries[i].position,
				elements,
			);
			drawStar(context, entries[i].position, 5, 2, 1, color);
			if (i > 0) {
				context.moveTo(entries[i - 1].position.x, entries[i - 1].position.y);
				context.lineTo(entries[i].position.x, entries[i].position.y);
				context.lineWidth = 3;
				context.strokeStyle = color;
				context.stroke();
			}
		}
	}
</script>

<script lang="ts">
	export let entries: TocEntry[];

	let canvas: HTMLCanvasElement;
	let parent: HTMLElement;
	let elements: HTMLElement[] = [];

	let isPlane = false;
	let color = '#28b0ff';
	let hrefPrefix = '';

	const onClick = () => {
		if (isPlane) {
			color = '#28b0ff';
			hrefPrefix = '';
		} else {
			color = '#ea580c';
			hrefPrefix = 'plane/';
		}

		isPlane = !isPlane;
	};

	$: drawToc(parent, canvas, entries, color, hrefPrefix, elements);
</script>

<div class="flex h-screen items-center justify-center bg-gray-800">
	<div
		bind:this={parent}
		class="crt-screen relative h-[550px] w-[700px] border-4 border-solid border-gray-700 bg-black shadow-2xl"
	>
		<div class="absolute bottom-2 left-2 z-30 flex items-center gap-2">
			<div
				class="h-10 w-10 cursor-pointer select-none rounded-lg"
				style={`background: ${isPlane ? '#28b0ff' : '#ea580c'}`}
				on:click={onClick}
				on:keydown={undefined}
			/>
			<div class="text-white">⇐ Click here to turn {isPlane ? 'on' : 'off'} styling</div>
		</div>
		<div class="absolute left-[50%] translate-x-[-50%] text-3xl text-white">
			Table of Contents
		</div>
		<canvas height="550" width="700" bind:this={canvas} />
	</div>
</div>
