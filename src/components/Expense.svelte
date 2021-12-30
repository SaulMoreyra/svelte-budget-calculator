<script>
  // import { getContext, createEventDispatcher } from "svelte";
  import { getContext } from "svelte";
  import {blur, slide, scale, fade, fly} from 'svelte/transition'

  export let id = null;
  export let name = "";
  export let amount = 0;

  let display = false;
  const {remove, modified} = getContext("expenses");

  function handleDisplayAmount() {  display = !display; }

  // const dispatch = createEventDispatcher();

</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={handleDisplayAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if display}
      <!-- <h4 transition:blur>amount: ${amount}</h4> -->
      <h4 transition:slide>amount: ${amount}</h4>
      <!-- <h4 transition:scale>amount: ${amount}</h4> -->
      <!-- <h4 transition:fade>amount: ${amount}</h4> -->
      <!-- <h4 transition:fly>amount: ${amount}</h4> -->
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn"  on:click={()=> modified(id)}>
      <i class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn" on:click={()=> remove(id)}>
      <i class="fas fa-trash" />
    </button>

    <!-- THIS IS IF YOU WANT TO USE AN EVENTDISPATCHER INSTED OF CONTEXT -->
    <!-- <button class="expense-btn delete-btn" on:click={()=> dispatch("delete", {id})}>
      <i class="fas fa-trash" />
    </button> -->
  </div>
</article>
