<script lang="ts">
	import TagInput from './Tags/TagInput.svelte';
	import TagList from './Tags/TagList.svelte';
	import { getContext } from 'svelte';
	import { user } from '$lib/stores';

	const i18n = getContext('i18n');

	export let tags = [];

	export let deleteTag: Function;
	export let addTag: Function;
</script>

{#if $user?.role === 'admin'}
	<div class="flex flex-row flex-wrap gap-1 line-clamp-1">
		<TagList
			{tags}
			on:delete={(e) => {
				deleteTag(e.detail);
			}}
		/>

		<TagInput
			label={tags.length == 0 ? $i18n.t('Add Tags') : ''}
			on:add={(e) => {
				addTag(e.detail);
			}}
		/>
	</div>
{/if}