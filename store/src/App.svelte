<script>
  import Cart from "./Cart/Cart.svelte";
  import Products from "./Products/Products.svelte";
  import Button from './UI/Button.svelte';
  import { timer } from './timer-store';
  import { name, greeting } from './store.js';

  let showCart = true;

  // timer.subscribe(count => {
  //   console.log('App:', count);
  // });
</script>

<h1>{$greeting}</h1>
<input bind:value={$name}>
 
<button on:click="{() => $name += '!'}">
    Add exclamation mark!
</button>

<Button on:click={() => { showCart = !showCart }}>Toggle Cart</Button>
{#if showCart}
  <Cart />
{/if}
<Products />

<!-- <p>Count: {$timer}</p> -->