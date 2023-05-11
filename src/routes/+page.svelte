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
	];
</script>

<TableOfContents {entries} />
