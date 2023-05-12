<script lang="ts">
	import TableOfContents from '$lib/organization/tableOfContents.svelte';

	const entries = [
		{
			title: 'Introduction',
			href: 'introduction',
			position: { x: 80, y: 55 },
		},
		{
			title: 'Note about Worksheets',
			href: 'worksheet-note',
			position: { x: 150, y: 120 },
		},
		{
			title: 'TED Talks',
			href: 'ted-talks',
			position: { x: 280, y: 100 },
		},
		{
			title: 'Research Journal',
			href: 'research-journal',
			position: { x: 310, y: 200 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 390, y: 250 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 370, y: 350 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 320, y: 320 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 350, y: 420 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 580, y: 520 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 620, y: 590 },
		},
		{
			title: 'WIP',
			href: 'WIP',
			position: { x: 690, y: 660 },
		},
	];
</script>

<TableOfContents {entries} />
