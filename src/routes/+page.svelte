<script lang="ts">
	import { onMount, type ComponentProps } from 'svelte';
	import Component from './component.svelte';
	import Motion from './motion.svelte';
	import RandomThing from './randomThing.svelte';
	import Table from './table.svelte';

	let game: HTMLCanvasElement;

	onMount(() => {
		const ctx = game.getContext('2d');
		if (!ctx) return;
		ctx.fillStyle = 'rgb(200, 0, 0)';
		ctx.fillRect(10, 10, 50, 50);

		ctx.fillStyle = 'rgba(0, 0, 200, 0.5)';
		ctx.fillRect(30, 30, 50, 50);
	});

	let value = 'Hello World';
	let width: null | number = null;
	let height: null | number = null;

	$: console.log(width, height);

	const props : ComponentProps<Component> = {name: "yolo", mit: "bolo"};
	const data = [
		{id: "1", name: "andreas"},
		{id: "2", name: "paul"},
		{id: "3", name: "karl"},
	];


	function clicked(e: Event, id: string) {
		console.log(id);
	}
</script>

<Motion />

<Component {...props} />

<div bind:offsetWidth={width} bind:offsetHeight={height}>
	<textarea
		on:input={() => console.log('Old value:', value)}
		bind:value
		on:input={() => console.log('New value:', value)}
	/>

	<canvas bind:this={game} />
</div>

<RandomThing inner={Component} />

<Table rows={data} let:item>
	<slot name="header">
		<tr>
			<th>Id</th>
			<th>Name</th>
			<th>-</th>
		</tr>
	</slot>
	<tr>
		<td>{item.id}</td>
		<td>{item.name}</td>
		<button on:click|preventDefault|stopPropagation={(e) => clicked(e, item.id)}>Click Me!</button>
	</tr>
</Table>
