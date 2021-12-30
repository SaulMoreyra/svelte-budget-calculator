<script>
  import Title from "./Title.svelte";
  export let addExpense;
  export let editExpense;
  export let closeForm;

  export let name = "";
  export let amount = null;
  export let isEditing;

  $: isEmpty = !name || !amount;

  function handleOnSubmit(event) {
    const expense = { name, amount };
    isEditing ? editExpense(expense) : addExpense(expense);
    name = "";
    amount = null;
    closeForm()
  }
</script>

<section class="form">
  <Title title={isEditing ? "edit expense" : "add expense"} />
  <form on:submit|preventDefault={handleOnSubmit} class="expense-form">
    <div class="form-control">
      <label for="name">Name</label>
      <input type="text" name="name" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">Amunt</label>
      <input type="number" name="amount" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">please fill out all form fields</p>
    {/if}
    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}
    >
      {#if isEditing}
        edit expense
      {:else}
        add expense
      {/if}
    </button>
    <button type="button" class="close-btn" on:click={closeForm}>
      <i class="fas fa-times" />
      close
    </button>
  </form>
</section>
