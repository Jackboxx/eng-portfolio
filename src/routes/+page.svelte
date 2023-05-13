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
			title: 'Self Evaluation',
			href: 'self-evaluation',
			position: { x: 370, y: 350 },
		},
	];
</script>

<TableOfContents {entries} />
