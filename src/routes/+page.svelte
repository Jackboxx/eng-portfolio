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
			title: 'Presentation',
			href: 'presentation',
			position: { x: 230, y: 250 },
		},
		{
			title: 'TED Talks',
			href: 'ted-talks',
			position: { x: 350, y: 120 },
		},
		{
			title: 'Research Journal',
			href: 'research-journal',
			position: { x: 400, y: 200 },
		},
		{
			title: 'Business Podcasts',
			href: 'business-podcasts',
			position: { x: 550, y: 280 },
		},
		{
			title: 'Self Evaluation',
			href: 'self-evaluation',
			position: { x: 590, y: 420 },
		},
	];
</script>

<div class="overflow-scroll bg-gray-800">
	<TableOfContents {entries} />
</div>
