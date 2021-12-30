<script>
  import { blur, slide, scale, fade, fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  import SectionTitle from "./Title.svelte";
  import Expense from "./Expense.svelte";
  export let expenses = [];
</script>

<section>
  <SectionTitle title="Expenses list" />
  <ul>
    <!-- THIS IS IF YOU WANT TO USE A EVENTDISPATCHER INSTED OF CONTEXT -->
    <!-- <Expense {...expense} on:delete/> -->
    {#each expenses as expense, index (expense.id)}
      <div
        in:fly={{ x: 200, delay: index * 700 }}
        out:fly={{ x: -200 }}
        animate:flip
      >
        <Expense {...expense} />
      </div>
    {:else}
      <h2>No expenses added to the list</h2>
    {/each}
  </ul>
</section>
