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
	];
</script>

<TableOfContents {entries} />
