<script>
	import Product from './Product.svelte';
	import CartItem from './CartItem.svelte';
	import FamliryNode from './FamliryNode.svelte';

	let y;

	$: console.log(y);

	let currentTitle = 'My app';

	let famliyStructure = [
		{ isParent: true, name: 'Chris', children: [
			{ isParent: true, name: 'Moe', children: [
				{ isParent: false, name: 'Julie' }
			] }	
		] },
		{ isParent: false, name: 'Anna' }
	]

	let renderdComponent = {cmp: Product, title: 'Test Product', id: 'p1' };

	function toggle() {
		if (renderdComponent.cmp === Product) {
			renderdComponent = {cmp: CartItem, title: 'Another Product', id: 'p2' };
		} else {
			renderdComponent = {cmp: Product, title: 'Test Product', id: 'p1' };
		}
	}

	function switchTitle() {
		currentTitle = 'A New Title';
	}
</script>

<style>
	div {
		height: 3000px;
	}
</style>

<svelte:window bind:scrollY={y} />
<svelte:body on:mouseenter />

<svelte:head>
	<title>{currentTitle}</title>
</svelte:head>

<button on:click={switchTitle}>Switch Title</button>

<div>
	<button on:click="{toggle}">Toggle Display</button>

	<svelte:component this={renderdComponent.cmp} title={renderdComponent.title} id={renderdComponent.id} />

	{#each famliyStructure as famliyMember}
		<FamliryNode member={famliyMember} />
	{/each}
</div>