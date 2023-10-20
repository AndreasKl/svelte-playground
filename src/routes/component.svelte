<script lang="ts">
	import { derived, writable } from 'svelte/store';
	const a = writable(21);

	const doubled = derived(a, ($a) => $a * 2);

	const delayed = derived(
		a,
		($a, set) => {
			setTimeout(() => set($a * 2), 1000);
		},
		$a
	);

	const delayedIncrement = derived<typeof a, number>(a, ($a, set, update) => {
		set($a);
		setTimeout(() => update((x) => x + 1), 2000);
	});

	export let name: string;

	$: console.log($$props);
</script>

<div>{name} {$a} {$doubled} {$delayed} {$delayedIncrement}</div>
<input type="number" bind:value={$a} />
