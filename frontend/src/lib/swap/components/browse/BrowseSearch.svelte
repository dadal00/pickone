<script lang="ts">
	import { PUBLIC_MAX_CHARS } from '$env/static/public'
	import { appState } from '$lib/swap/AppState.svelte'
	import { ItemFields, type Condition, type ItemType, type Location } from '$lib/swap/models'
	import { onDestroy, onMount } from 'svelte'
	import SearchFilters from './SearchFilters.svelte'

	let query: string = $state('')
	let itemTypeFilter: ItemType | '' = $state('')
	let locationFilter: Location | '' = $state('')
	let conditionFilter: Condition | '' = $state('')

	onMount(() => {
		const fullQuery = appState.getFullQuery()
		query = fullQuery.query
		itemTypeFilter = fullQuery[ItemFields.ITEM_TYPE]
		locationFilter = fullQuery[ItemFields.LOCATION]
		conditionFilter = fullQuery[ItemFields.CONDITION]
	})

	$effect(() => {
		appState.setQuery(query)
		appState.setItemTypeFilter(itemTypeFilter)
		appState.setLocationFilter(locationFilter)
		appState.setConditionFilter(conditionFilter)
	})

	onDestroy(() => {
		appState.setQuery('')
		appState.setItemTypeFilter('')
		appState.setLocationFilter('')
		appState.setConditionFilter('')
		appState.setOffset(0)
	})
</script>

<h1 class="text-3xl font-bold mb-8">Browse All Items</h1>
<div class="bg-white rounded-lg shadow-sm border p-6 mb-8">
	<div class="flex flex-col lg:flex-row gap-4">
		<div class="flex-1 relative">
			<input
				type="text"
				placeholder="Search for items..."
				class="w-full pl-10 pr-4 py-3 border rounded-lg"
				maxlength={Number(PUBLIC_MAX_CHARS)}
				bind:value={query}
			/>
			<span class="absolute left-3 top-1/2 transform -translate-y-1/2">🔍</span>
		</div>
		<SearchFilters bind:itemTypeFilter bind:locationFilter bind:conditionFilter />
	</div>
	<div class="flex items-center justify-between mt-4 pt-4 border-t">
		<p class="text-gray-600">{appState.getTotalHits()} items available</p>
	</div>
</div>
