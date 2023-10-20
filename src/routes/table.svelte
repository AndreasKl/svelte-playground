<script lang="ts">
	export let rows: T[];

	type T = $$Generic<{ id: string|number }>;
</script>

<table>
	<tbody>
		{#each rows as row (row.id)}
			<slot item={row}></slot>
		{/each}
	</tbody>
</table>
