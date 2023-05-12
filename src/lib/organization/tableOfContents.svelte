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
		parent.appendChild(element);
	}

	function drawStar(
		ctx: CanvasRenderingContext2D,
		position: { x: number; y: number },
		spikes: number,
		outerRadius: number,
		innerRadius: number,
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
		ctx.strokeStyle = '#28b0ff';
		ctx.stroke();
		ctx.fillStyle = '#28b0ff';
		ctx.fill();
	}

	function drawToc(
		parent: HTMLElement,
		canvas: HTMLCanvasElement | undefined,
		entries: TocEntry[],
	) {
		if (!canvas) return;
		const context = canvas.getContext('2d');
		if (!context) return;

		for (let i = 0; i < entries.length; i++) {
			createTocEntryElement(
				parent,
				entries[i].title,
				entries[i].href,
				entries[i].position,
			);
			drawStar(context, entries[i].position, 5, 2, 1);
			if (i > 0) {
				context.moveTo(entries[i - 1].position.x, entries[i - 1].position.y);
				context.lineTo(entries[i].position.x, entries[i].position.y);
				context.lineWidth = 3;
				context.strokeStyle = '#28b0ff';
				context.stroke();
			}
		}
	}
</script>

<script lang="ts">
	export let entries: TocEntry[];

	let canvas: HTMLCanvasElement;
	let parent: HTMLElement;

	$: drawToc(parent, canvas, entries);
</script>

<div class="flex h-screen items-center justify-center bg-gray-800">
	<div
		bind:this={parent}
		class="crt-screen relative h-[700px] w-[700px] border-4 border-solid border-gray-700 bg-black shadow-2xl"
	>
		<div class="absolute left-[50%] translate-x-[-50%] text-3xl text-white">
			Table of Contents
		</div>
		<canvas height="700" width="700" bind:this={canvas} />
	</div>
</div>
