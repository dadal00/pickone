<script lang="ts">
	import Mission from '$lib/swap/components/about/Mission.svelte'
	import Story from '$lib/swap/components/about/Story.svelte'
	import Values from '$lib/swap/components/about/Values.svelte'
</script>

<svelte:head>
	<title>About - BoilerSwap</title>
</svelte:head>

<div class="container mx-auto px-6 py-16 max-w-4xl">
	<div class="text-center mb-16">
		<h1 class="text-4xl font-bold text-gray-900 mb-4">About BoilerSwap</h1>
		<p class="text-xl text-gray-600">
			Building a sustainable community at Purdue, one item at a time
		</p>
	</div>

	<Mission />
	<Story />
	<Values />
</div>
