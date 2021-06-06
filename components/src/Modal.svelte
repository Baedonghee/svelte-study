<script>
  import { createEventDispatcher, onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';

  const dispatch = createEventDispatcher();

  let agree = false;
  let autoScroll = false;

  onMount(() => {
    console.log('onMount');
  })

  onDestroy(() => {
    console.log('onDestory');
  })

  beforeUpdate(() => {
    console.log('beforeUpdate');
    autoScroll = agree;
  })

  afterUpdate(() => {
    console.log('afterUpdate');
    if (autoScroll) {
      const modal = document.querySelector('.modal');
      modal.scrollTo(0, modal.scrollHeight);
    }
  })

  console.log('Script executed!!');
</script>

<style>
  .backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.75);
    z-index: 10;
  }

  .modal {
    padding: 1rem;
    position: fixed;
    top: 10vh;
    left: 10%;
    width: 80%;
    max-height: 10vh;
    background: white;
    border-radius: 5px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    overflow: scroll;
  }

  header {
    border-bottom: 1px solid #ccc;
  }
</style>

<div class="backdrop" on:click="{() => dispatch('cancel')}"/>
<div class="modal">
  <header>
    <!-- 지정한 슬롯에만 -->
    <slot name="header" />
  </header>
  <div class="content">
    <!-- 지정하지 않으면 모든 슬롯 -->
    <slot />
  </div>
  <div class="disclaimer">
    <p>Before you close, you need to agree to our terms!</p>
    <button on:click="{() => agree = true}">Agree</button>
  </div>
  <footer>
    <slot name="footer" didAgree={agree}>
      <button on:click="{() => dispatch('close')}" disabled={!agree}>Close</button>
    </slot>
  </footer>
</div>