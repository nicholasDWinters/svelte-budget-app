<script lang="ts">
  import Navbar from '../components/Navbar.svelte';
  import ExpensesList from '../components/ExpensesList.svelte';
  import expensesData from '../expenses';
  import ExpenseForm from '../components/ExpenseForm.svelte';
  import type { TypeExpense } from '../types';

  let expenses = [...expensesData];
  let inProgress: TypeExpense;
  $: expenses;
  $: inProgress;
  // dispatching events - create function in parent component (removeExpense), takes an event, contains 'details' which will hold our info that we pass through, use on:remove on the child component, use event forwarding through all other components using on:remove, and then in final child componet, Expense.svelte, create event dispatcher, and dispatch the remove event, passing through the id we need

  let removeExpense = (event: CustomEvent) => {
    expenses = expenses.filter(item => item.id !== event.detail?.id);
  }

  let clearExpenses = () => {
    expenses = [];
  }

  let addExpense = (event: CustomEvent) => {
    expenses = [event.detail.expense, ...expenses];

  }
  let editExpense = (event: CustomEvent) => {
    let expense = event.detail.expense;
    inProgress = expense;
    console.log(inProgress);
  }


</script>

<Navbar />
<main class="content">
  <ExpenseForm on:add={addExpense} current={inProgress} />
  <ExpensesList {expenses} on:remove={removeExpense} on:edit={editExpense} />
  <button on:click={clearExpenses} type='button' class="btn btn-primary btn-block">clear expenses</button>
</main>

<style>
  
</style>