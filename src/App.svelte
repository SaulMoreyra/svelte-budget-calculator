<!-- SCRIPT -->
<script>
  import { afterUpdate, onMount, setContext } from "svelte";

  import GithubAwait from "./components/GithubAwait.svelte";
  import Github from "./components/Github.svelte";
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import Totals from "./components/Totals.svelte";
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import Modal from "./components/Modal.svelte";

  import expensesData from "./utils/expenses";

  const defaultExpense = { name: "", amount: null, id: null };

  //VARIABLES
  let expenses = [];
  let editableExpense = { ...defaultExpense };
  let isFormOpen = false;

  //REACTIVE
  $: total = expenses.reduce((acc, expense) => acc + expense.amount, 0);
  $: isEditing = Boolean(editableExpense.id);

  //FUNCTIONS

  function showForm() {
    isFormOpen = true;
  }

  function closeForm() {
    isFormOpen = false;
    editableExpense = { ...defaultExpense };
  }

  function deleteExpense(id) {
    expenses = expenses.filter((expense) => expense.id !== id);
  }

  function clearExpenses() {
    expenses = [];
  }

  function addExpense({ name, amount }) {
    const newExpense = { id: Math.random(), name, amount };
    expenses = [newExpense, ...expenses];
  }

  function setModifiedExpense(id) {
    showForm();
    editableExpense = expenses.find((expense) => expense.id === id);
  }

  function editExpense({ name, amount }) {
    expenses = expenses.map(({ id, ...rest }) =>
      editableExpense.id === id ? { id, name, amount } : { id, ...rest }
    );
    editableExpense = { ...defaultExpense };
  }

  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }

  onMount(() => {
    const storageExpenses = localStorage.getItem("expenses");
    expenses = storageExpenses ? JSON.parse(storageExpenses) : [];
  });

  afterUpdate(() => {
    setLocalStorage();
  });

  //CONTEXT
  setContext("expenses", {
    remove: deleteExpense,
    modified: setModifiedExpense,
  });

  /** THIS IS IF YOU WANT TO USE A EVENTDISPATCHER INSTED OF CONTEXT */
  // function deleteExpenseDispatch(event){
  //   const {id} = event.detail;
  //   deleteExpense(id)
  // }
</script>

<!-- HTML -->
<Navbar {showForm} />
<main class="content">
  {#if isFormOpen}
    <Modal>
      <ExpenseForm
        {addExpense}
        {editExpense}
        {closeForm}
        {isEditing}
        name={editableExpense.name}
        amount={editableExpense.amount}
      />
    </Modal>
  {/if}
  <Totals title="total expenses" {total} /> -->
  <!-- THIS IS IF YOU WANT TO USE A EVENTDISPATCHER INSTED OF CONTEXT -->
  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}
  >
    clear expenses
  </button>

  <GithubAwait />
  <Github />
</main>
